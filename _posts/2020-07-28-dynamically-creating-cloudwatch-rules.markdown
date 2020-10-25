---
layout: post
title:  "Dynamically create CloudWatch Rules to let users schedule recurring actions"
date:   2020-07-28 08:05:00 +0000
categories: serverless
slug: dynamically-create-cloudwatch-rules
canonical_url: 'https://miksimal.com/dynamically-create-cloudwatch-rules'
---

I recently needed to build a feature to let users set their own frequency for a recurring action. Specifically, I wanted to let the user decide how often my app should randomly pair members of their organisation and connect them via email.

I couldn't find many resources on how to easily accomplish this with serverless on AWS, so thought I'd share my learnings and explain the approach I took.

In short, I have an API Gateway / Lambda endpoint which both:
+ Adds or updates a CloudWatch Rule with the desired frequency. This rule will then trigger a Lambda (when it's time) which pairs and emails organisation members.

+ Adds or updates a 'RecurrenceRule' DynamoDB item (I store this here to make it easy to display to the user what their current setting is).


Visually, it could look e.g. like this with a simple dropdown:

![The end result: selecting a frequency updates a CW rule](/assets/end-result-set-frequency.gif)

<br />

In this post, I'll explain how I implemented the backend side of this, using The Serverless Framework, API Gateway, Lambda, and CloudWatch.

**Note:** there may very well be better ways to achieve this. In fact, I'm secretly hoping that by sharing my approach here I will get some feedback to improve my solution, so please reach out if you've got ideas!

<br />

### Write a 'ManageRecurrenceRules' Lambda

First, write a Lambda function which manages the recurrence rules. This is the one that will be triggered by users clicking in the dropdown example above.

We will need the clients for both DynamoDB and CloudWatch as well as an environmental variable:

``` javascript
const dynamoDb = new AWS.DynamoDB.DocumentClient();
const cloudWatch = new AWS.CloudWatchEvents();
const recurringPairAndEmailFunctionArn = process.env.RECURRING_PAIRANDEMAIL_LAMBDA_ARN;
```

Ignoring various other things you may want to do (e.g. I retrieve an organisationId from Cognito), we first need to construct a cron expression based on the POST request, e.g.:

``` javascript
const frequency = JSON.parse(event.body);

let scheduleExpression;
switch(frequency) {
    case 'Fridays':
      scheduleExpression = "cron(0 12 ? * FRI *)";
      break;
    case 'Every 5 Minutes':
      scheduleExpression = "cron(0/5 * * * ? *)";
      break;
    case 'Daily':
      scheduleExpression = "cron(0 12 * * ? *)";
      break;
    default:
      // return an 'Invalid frequency' error to the user;
```

Next, we need to construct a unique rulename. I used an organisationId (which I get from an `adminGetUser` Cognito request) combined with the stage:

``` javascript
const ruleName = organisationId + "-" + process.env.STAGE;
```

Use `putRule` to create or update the rule and then use `putTargets` to add the desired target Lambda we want the rule to trigger in my case a Lambda function that pairs organisation members and email-intros each pair:

``` javascript
  try {
    await cloudWatch.putRule({
      Name: ruleName,
      ScheduleExpression: scheduleExpression
    }).promise();

    await cloudWatch.putTargets({
      Rule: ruleName,
      Targets: [
        {
          Id: organisationId,
          Arn: recurringPairAndEmailFunctionArn,
          Input: JSON.stringify({
            organisationId: organisationId
          }) // the rule will pass this Input to the Lambda when it triggers it
        }
      ]
    }).promise();
```

Note that I tell the rule to pass a custom Input to the Lambda target. This means that the target, in my case the 'recurringPairAndEmailFunction', can access the property directly from the event like this:


``` javascript
const orgId = event.organisationId;
```


Finally, still in the same 'try/catch' block, I add this rule to DynamoDB to easily display the currently selected frequency to the user:
``` javascript
    const params = {
      TableName: process.env.USERS_TABLE,
      Item: {
        PK: organisationId,
        SK: "RecurrenceRule",
        frequency: frequency
      }
    };
    await dynamoDb.put(params).promise();
```

If all this goes well, we return a lovely 200 OK to the user 🎉

<br />

### serverless.yml setup

Next, we need to define the API Gateway endpoint and pass the environmental variable to the Lambda (the `recurringPairAndEmailFunctionArn` used above). In the serverless.yml:

``` yaml
  manageRecurrenceRules:
    handler: manageRecurrenceRules.main
    environment:
      RECURRING_PAIRANDEMAIL_LAMBDA_ARN: arn:aws:lambda:${self:provider.region}:accountidgoeshere:function:${self:service}-${self:custom.stage}-recurringPairAndEmail
    events:
      - http:
          path: rules
          method: post
          cors: true
          authorizer: aws_iam
```

Note that the target Lambda, recurringPairAndEmail, is defined in the template as simply:
``` yaml
  recurringPairAndEmail:
    handler: recurringPairAndEmail.main
```

Next, we need to make sure that our Rules have the required permissions to invoke our Lambda. The below allows all rules for my account in this region to invoke the Lambda (which is probably too permissive):

``` yaml
resources:
  - Resources:
      RecurringPairAndEmailInvokePermission:
        Type: AWS::Lambda::Permission
        DependsOn: RecurringPairAndEmailLambdaFunction
        Properties:
          Action: lambda:InvokeFunction
          Principal: events.amazonaws.com
          SourceArn:
            Fn::Sub: "arn:aws:events:${self:provider.region}:accountidgoeshere:rule/*"
          FunctionName: arn:aws:lambda:${self:provider.region}:accountidgoeshere:function:${self:service}-${self:custom.stage}-recurringPairAndEmail
```

Finally, we need to ensure that our 'ManageRecurrenceRules' Lambda has permissions to add rules and targets, so we add the below in the `provider` section:

``` yaml
iamRoleStatements:
    - Effect: "Allow"
      Action:
        - events:putRule
        - events:putTargets
```
<br />

### Aaand, that's it!
Our users can now choose between Fridays, Daily or Every 5 Minutes as frequencies by making a POST request to the /rules path.

In CloudWatch, a rule will look something like this:

![the resulting rule in CloudWatch for emails every Friday](/assets/the-result-in-cloudwatch.png)

<br />

### How can the solution be improved? Is this the 'right' way?
Now, back to my secret intention with this blog post... How can the solution be improved? Is this the 'right' way of implementing this feature?

How can I best work around the constraints on CloudWatch Rules, such as:

+ The per-region *soft* limit of 100 CW Rules.

+ The limit of 5 targets per rule (e.g. so having a rule for each frequency and adding organisations as Input probably isn't the way either).

**Thanks for reading and I hope to hear from you either here or on Twitter (<a href="https://twitter.com/miksimal" target="_blank">@miksimal</a>)!**
---
layout: post
title:  "How to quickly set up a Cognito User Pool with custom attributes in the Serverless Framework and create a test user"
excerpt: "Notes for my future self and whomever else this may concern!"
date:   2020-06-08 20:28:00 +0000
categories: serverless
slug: cognito-attributes-howto
canonical_url: 'https://miksimal.com/cognito-attributes-howto'
---

Yesterday, I was setting up a Cognito User Pool in my Serverless project and found two things slightly more time consuming than they should have been:
+ adding pre-defined attributes such as first name and family name to my users
+ adding a custom attribute, such as hacker name, to my users (and *attempting* to make it required)
+ adding a Lambda to use with the PreSignUp Cognito trigger to perform custom validation
+ creating and verifying a test user

This was due to a combination of the usual impenetrable AWS documentation and a lack of code examples for this specific thing in the Serverless Framework docs, so I thought I'd share an example here that may help others as well as my future self.

Firstly, the secret to adding attributes to a User Pool is that the attributes need to be defined under the *Schema* property.

With that in mind, <a href="https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-cognito-userpool.html" target="_blank">this documentation in hand</a>, here is an example of creating a user pool with email as username and alias, and a schema that additionally takes last name and first name (both required):

``` yaml
Resources:
  CognitoUserPool:
    Type: AWS::Cognito::UserPool
    Properties:
      UserPoolName: ${self:custom.stage}-user-pool
      UsernameAttributes:
        - email
      AutoVerifiedAttributes:
        - email
      Schema:
        - Name: "family_name"
          Required: true
          Mutable: true
        - Name: "name"
          Required: true
          Mutable: true
```

So, what if we wanted to add a custom attribute (i.e. one that AWS has not predefined for us, unlike name and family_name)? Let's say we want to require users to provide a "hacker_name" in addition to the other names. We'll provide an AttributeDataType as this won't be predefined.

``` yaml
...
      Schema:
        - Name: "family_name"
          Required: true
          Mutable: true
        - Name: "name"
          Required: true
          Mutable: true
        - Name: "hacker_name"
          Required: true
          Mutable: true
          AttributeDataType: String
```
Trying to deploy this, you'll get an error like:

``` bash
An error occurred: CognitoUserPool - Required custom attributes are not supported currently.
```

It turns out that *you cannot set custom attributes as required in Cognito*. So you'll either have to make do with the attributes that AWS gives you (maybe "hacker name" could be replaced by "nickname", e.g.), leave the attribute as optional, or find other workarounds. The most obvious workaround that comes to mind is to use Cognito's PreSignUp trigger and use a Lambda for validation of the attributes. In the template, that would look something like this in the User Pool definition:

``` yaml
...
      Schema:
        - ...
      LambdaConfig:
        PreSignUp: "${self:provider.environment.PRE_SIGNUP_LAMBDA}"
```

Where we've defined the PRE_SIGNUP_LAMBDA is the arn of the Lambda that performs the validation, for example:
``` yaml
provider:
  name: aws
  runtime: nodejs12.x
  stage: dev
  region: eu-west-1
  environment:
    PRE_SIGNUP_LAMBDA: arn:aws:lambda:${self:provider.region}:yourawsaccountnumbergoeshere:function:${self:service}-${self:provider.stage}-preSignup
functions:
  preSignup:
    handler: preSignup.main
```

Phew! Now, we're ready to get some work done! Except, you made a small typo in one of the attributes (e.g. you no longer want "family_name" to be required). Luckily, that is easy to fix: **to change an attribute, you simply delete the entire user pool and create a new one 🤯.**

Yep, as the friendly terminal output will tell you, you cannot modify existing attributes, so think carefully the first time!
``` bash
An error occurred: CognitoUserPool - Existing schema attributes cannot be modified or deleted.
```

Now finally, with all that work, having deleted and recreated our user pool a few times, adding custom validation, etc. we are ready to add a test user and try this thing out!

Surely, this at least, should be easy. No need to worry about infrastructure as code. Just click the friendly 'Create user' button in the AWS Console, right?

*Wrong*!

Adding a user, the Account status will be set to `FORCE_CHANGE_PASSWORD`. Although friendly-looking, this is not good.

![Adding a User in the AWS Console, they'll have a "FORCE_CHANGE_PASSWORD" account status](/assets/cognitoForceChangePassword.png)

If you try to use this test user *as is* you might be able to log in on your site, but then get logged out immediately or lack the privileges you'd expect to have been granted to the user.

There is no easy way to fix this in the GUI, so the fastest and best way to create and verify a test user is to use the AWS CLI. Here are the two relevant commands:

First, create the user (could also be done in the AWS Console as above of course):
```
aws cognito-idp sign-up \
--region eu-west-1 \
--client-id HereGoesTheAppClientId \
--username mikkel.examplemail@gmail.com \
--user-attributes Name=name,Value=Mikkel Name=family_name,Value=Lauritzen \
--password DESIREDPASSWORDHERE
```

Second, confirm the user (i.e. get rid of our friendly `FORCE_CHANGE_PASSWORD`):
```
aws cognito-idp admin-confirm-sign-up \
--region eu-west-1 \
--user-pool-id eu-west-dasdsadasdasdasdbALdlsa \
--username mikkel.examplemail@gmail.com
```

*Now*, you're good to go with a functioning test user.



I hope this guide saves you (and my future self) some of the pain I went through when starting out with Cognito. In the end, it just may be worth it given the price of ~$0 / mo for my needs and the tight integration with the rest of my serverless stack on AWS.
---
layout: post
title:  "How to quickly set up a Cognito User Pool with custom attributes in the Serverless Framework and create a test user"
excerpt: "Example serverless.yml code for how to add user attributes. Commands for quickly creating and verifying a test user."
date:   2020-06-08 20:28:00 +0000
categories: serverless
slug: cognito-attributes-howto
canonical_url: 'https://miksimal.com/cognito-attributes-howto'
---

Yesterday, I was setting up a Cognito User Pool in my Serverless project and found two things slightly more time consuming than they should have been:
+ adding attributes such as first name and family name to my users
+ creating and verifying a test user (do *not* do this in the AWS GUI!)

This was due to a combination of the usual impenetrable AWS documentation and a lack of code examples for this specific thing in the Serverless Framework docs, so I thought I'd share an example here that may help others as well as my future self.

Firstly, the secret to adding attributes to a User Pool is that the attributes need to be defined under the *Schema* property.

With that in mind, <a href="https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-cognito-userpool.html" target="_blank">this documentation in hand</a>, and knowing what a List looks like in YAML(!), here is an example of creating a user pool with email as username and alias, and a schema that additionally takes last name and first name (both required):

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

With that user pool created, the first thing you'll want to do is to create a test user! That, at least, should be easy. No need to worry about infrastructure as code. We'll just head to the AWS Console and create a user, right?

*Wrong*!

Just adding a user, the Account status will be set to `FORCE_CHANGE_PASSWORD`. Although friendly-looking, this is not good.

![Adding a User in the AWS Console, they'll have a "FORCE_CHANGE_PASSWORD" account status](/assets/cognitoForceChangePassword.png)

Specifically, if you try to use this test user as is you might be able to log in on your site, but then get logged out immediately or lack the privileges you'd expect to have been granted to the user.

There is no easy way to fix this in the GUI, so the fastest and best way to create and verify a test user is going to be using the AWS CLI. Here are the two relevant commands:

First, create the user (could also be done in the GUI of course):
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
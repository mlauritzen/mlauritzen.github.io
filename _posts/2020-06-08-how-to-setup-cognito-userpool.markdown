---
layout: post
title:  "How to set up Cognito User Pool attributes (e.g. first name) in the Serverless Framework"
excerpt: "Example serverless.yml code for how to add user attributes, using the Schema attribute."
date:   2020-06-08 20:28:00 +0000
categories: serverless
slug: cognito-attributes-howto
canonical_url: 'https://miksimal.com/cognito-attributes-howto'
---

Yesterday, I was setting up a Cognito User Pool in my Serverless project and found it slightly more time consuming than expected to figure out the syntax for adding user attributes such as first name and family name.

This was due to a combination of the usual impenetrable AWS documentation and a lack of code examples for this specific thing in the Serverless Framework docs, so I thought I'd share an example here that may help others as well as my future self.

The secret is that attributes are (suddenly) called <i>schema attributes</i> and are defined in a list under the <i>Schema</i> attribute in the template.

With that in mind, <a href="https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-cognito-userpool.html" target="_blank">this documentation in hand</a>, and knowing what a List looks like in YAML, here is an example of creating a user pool with email as username and alias, and a schema that additionally takes last name and first name (both required):

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
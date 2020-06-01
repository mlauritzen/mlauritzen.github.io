---
layout: post
title:  "Sentimental Robot reads the news"
excerpt: "Scraping and sentiment analysing BBC headlines every day, using Cloudwatch, Comprehend, DynamoDB, CloudFront, s3, API Gateway, and Lambda."
date:   2020-05-24 15:00:00 +0000
categories: serverless
slug: sentimental-robot
canonical_url: 'https://miksimal.com/sentimental-robot'
---

I recently completed a small project to get back into working with serverless and to learn about Amazon Comprehend.

In AWS's own words, Comprehend 'is a natural language processing (NLP) service that uses machine learning to find insights and relationships in text.'

Using this and a few other services, I created a <a href="https://sentimentalrobot.miksimal.com/" target="_blank">sentimental robot which reads the news</a>. More precisely, it grabs the top 10 BBC headlines each morning, chugs them into Comprehend for a sentiment analysis, and lets the user see the past few days' analyses.

I might publish a more detailed walk-through of how this was built, but below are my high-level notes.

### Backend: Lambda, Comprehend, Cloudwatch, DynamoDB, and API Gateway

#### Collecting, analysing and storing the headlines

A Cloudwatch Rule is set to trigger a Lambda function to run every day at 10AM. 

This Lambda function scrapes the top 10 headlines from the BBC's website (bbc.co.uk). It then invokes a second Lambda function, providing it the 10 headlines.

This second Lambda (written in Python) uses Amazon Comprehend to analyse the sentiment of the headlines and then gives back the resulting analysis to the first Lambda.

Finally, the first Lambda posts the headlines along with a date and the sentiment analysis to a table in DynamoDB.

#### Allowing the frontend to query the headlines database table

Through API Gateway, I made available the endpoint https://gp7dnv8i52.execute-api.eu-west-1.amazonaws.com/dev/getlatestbbc/ that the client can make GET requests to.

A GET request to this endpoint triggers a Lambda which queries the DynamoDB table for the headlines and analyses returns them to the requester in reverse chronological order.

### Frontend and hosting/distribution: React, Bootstrap, s3, and CloudFront

The frontend is a very simple React app, using React Bootstrap for styling (in particular, for the 'Accordion' that displays the result for each day and more info when clicked).

It's hosted out of an s3 bucket and distributed globally through CloudFront.

Not having used s3 for hosting a website before, and having never used CloudFront at all, I googled around and found an excellent resource that made it super simple: <a href="https://serverless-stack.com/chapters/deploying-a-react-app-to-aws.html" target="_blank">Serverless Stack</a> -- highly recommend it and wish I'd had the whole guide much earlier!

I found an error in the guide and since I found it so valuable I used this as an opportunity to make <a href="https://github.com/AnomalyInnovations/serverless-stack-com/pull/479" target="_blank">my first (small) open source contribution</a>.


### Potential next steps / stuff that is broken

Sentiment analysis seems weird sometimes... Is today really positive?

Can't continue to just give back all results. Will probably just restrict to the last seven days for now to keep things simple, but in a future project maybe there's something interesting to be done with the increasing amount of data I have available.
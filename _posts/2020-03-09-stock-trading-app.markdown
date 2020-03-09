---
layout: post
title:  "CalmStocks: A simple stock price alerts web app, using Angular, the IEX API, and serverless AWS services."
date:   2020-03-09 16:57:00 +0000
categories: learning
---

# CalmStocks: A simple stock price alerts web app, using Angular, the IEX API, and serverless AWS services.

### Quicklinks
 - [Introduction](#introduction)
 - [Features](#features)

## Introduction

This is a simple stock price alerts web app, using Angular, IEX's API for stock price data, and serverless AWS services on the backend (Cognito, Lambda, AppSync/GraphQL, DynamoDB). Twice a day, it checks each user's high/low alerts against real stock prices and alerts them via email if the threshold is reached.

## Features

- GraphQL Mutations (`src/app/graphql/mutations`)
  - Create new alert
  - Delete an alert

- GraphQL Queries (`src/app/graphql/queries`)
  - Get all of a user's alerts

- Authentication
  - The app uses Cognito User Pools to sign up users and authenticate them
  
- Authorization
  - The app uses JWT Tokens from Cognito User Pools as the authorization mechanism

## Getting Started

#### Prerequisites

* [AWS Account](https://aws.amazon.com/mobile/details) with appropriate permissions to create the related resources
* [NodeJS](https://nodejs.org/en/download/) with [NPM](https://docs.npmjs.com/getting-started/installing-node)
* [Angular CLI](https://github.com/angular/angular-cli) `(npm install -g @angular/cli)`

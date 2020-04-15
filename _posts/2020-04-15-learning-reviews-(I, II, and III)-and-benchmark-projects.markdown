---
layout: post
title:  "Learning reviews (I, II, and III) and benchmark projects"
date:   2020-04-15 08:37:00 +0000
categories: learning
---

Since I started learning to code, I have done occassional learning "reviews" where I take stock of what I've learnt and decide what I should learn next (and how).

I try to keep all of my learning objectives focused on "benchmark projects". I choose an output or accomplishment as my goal. So instead of "Learn about AWS", I would go for "Achieve an AWS certification". Instead of "Learn about node modules", it could be "Create my own simple NPM module and write about it". This approach is great because it:
+ motivates me as there is now a very clear finish line,
+ forces me to push through the hard and uncomfortable aspects of the learning to get to the end goal,
+ gives me a concrete achievement or "thing" that I can point to after achieving each goal.

[Scott Young has written about this](https://www.scotthyoung.com/blog/2019/11/15/drill-or-benchmark/).

To keep me accountable to continuing a high pace of learning, I'll start posting them here. I'm now at my fourth big review. Before posting about that, below are brief summaries of my first three reviews:

## Learning review, Rd. I (benchmark achieved: landed my first dev job)

Will do a more thorough write-up of what I did to get myself to a hireable level. The main resources I used were:

- Harvard CS50 course
- React course from udemy
- Eloquent Javascript book
- Coding challenges on Leetcode
- Listened to A LOT of podcasts, e.g. the first 250 episodes of Codepen Radio and most episodes of Syntax.

I got an opportunity to get a junior dev job very quickly for which the interview process involved three trial days of writing Android apps in Kotlin, 
so I also picked up some Kotlin specific resources such as "Kotlin Programming: The Big Nerd Ranch Guide".

I got the job, so the next learning goal was to become a productive junior dev quickly.


## Learning review, Rd. II (benchmark achieved: became a productive junior dev)

At the new job, the role quickly changed from writing Android apps to setting up backend infrastructure on AWS to work with an iOS app.

Learning included: setting up a NoSQL database (DynamoDB) with a GraphQL API, push notifications using Lambdas, converting infrastructure to CloudFormation templates, Node.js (picked up Wes Bos' Node course), and Swift/iOS (raywenderlich.com courses).

I even wrote my first bash script to automate some folder creation/deletion and config edits needed every time we did a codegen related to using the GraphQL API on the iOS frontend.

Overall I learned LOTS, covered a lot of fundamentals, and went from feeling like an imposter to feeling like I could add real value as an engineer. Outside of work, I read "Grokking Algorithms" and "Cracking the Coding Interview" to fill my algo/datastructures gaps.

Although I learnt a lot at work, we were a team of quite junior people (most had - unlike me - graduate degrees in computer science, but still). This meant that knowledge of best practices and of industry standards was somewhat limited.
I therefore decided that the next step in my learning would be to get involved in the dev community and to expand the breadth of my knowledge of AWS services and best practices by taking the AWS Solutions Architect certification.

## Learning review, Rd. III (benchmarks achieved: community + AWS certified)

Went to my first tech meet-up. Achieved AWS Solutions Architect Associate certification with just one month of study (AWS recommends at least "One year of hands-on experience designing available, cost-efficient, fault-tolerant, and scalable distributed systems on AWS" -- that is, I had to study hard for this exam!).

Getting to the level of understanding and knowledge where I could pass the AWS exam made me significantly more productive. I could now fluently discuss database types, trade-offs between hosting on EC2 instances vs. going fully serverless, autoscaling groups, the benefits/usecases of queuing systems like SQS. I also knew A LOT about moving from on-premise to cloud and managing a hybrid setup as well as lots of specifics about how Security Groups, Network Access Control Lists, private subnets, VPCs, internet gateways etc. come together -- none of which I really needed to know quite yet!

Not long after, I got talking to a very experienced CTO at an exciting fintech start-up that my friend - who I've long wanted to work with - had just joined... And the rest is history!

I was given more than 80 hours worth of training (video courses and books) to complete and would be diving into an unfamiliar infrastructure (C#/.NET and Angular), so again the benchmark project until the next review was: "Become a productive junior dev".

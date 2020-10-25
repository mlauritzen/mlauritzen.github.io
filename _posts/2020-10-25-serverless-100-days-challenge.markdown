---
layout: post
title: "Resources, projects, and lessons from 100 days of (serverless) cloud learning"
date: 2020-10-25 011:37:00 +0000
categories: serverless
slug: 100daysofserverless
canonical_url: 'https://miksimal.com/100daysofserverless'
---

I recently completed my challenge of spending at least 1 hour a day learning about (serverless) cloud for 100 days <i>almost</i>* in a row.

In this post, I summarise the main topics I covered and the best resources for each, the projects I built, and some lessons for future self-directed learning projects.

*It took me 114 days - with a pandemic and some vacation time thrown in, that's close enough I think!

## Topics and resources
The topics that I spent the most time on and found the best resources for were:
1. Fundamentals and the serverless landscape

2. Data modelling with DynamoDB

3. Best practices and design patterns

4. The business case for 'serviceful serverless'

### **Fundamentals and the serverless landscape**
Despite having an AWS SAA cert and having used AWS at work before the challenge, a key focus for me was gaining a stronger foundation by really understanding the serverless landscape, including tools, best practices, and design patterns.

For this, my favourites were:
- <a href="https://offbynone.io/" target="_blank">Off-by-none</a>: Jeremy Daly's weekly serverless newsletter. More resources than you have time to read, but always some great stuff for all levels in there.

- <a href="https://serverless-stack.com/" target="_blank">Serverless Stack</a>: an excellent, free resource that gets you going with building a full-stack project using React and Serverless Framework. Having an opinionated guide with links to further best practices and little tricks (like <a href="https://serverless-stack.com/chapters/mapping-cognito-identity-id-and-user-pool-id.html" target="_blank">this one</a>) was a life-saver.

- <a href="https://github.com/aws-samples/aws-serverless-airline-booking" target="_blank">Serverless Airline Booking</a> and its accompanying <a href="https://github.com/aws-samples/aws-serverless-airline-booking/tree/twitch" target="_blank">Twitch streams</a> (14+ hours of content). Covers a lot of ground despite not assuming much prior knowledge.

- <a href="https://theburningmonk.com/2020/03/announcing-the-new-real-world-serverless-podcast/" target="_blank">Real-World Serverless</a>: no fluff podcast that goes in-depth on best practices, architectures, and more. I have listened to *all* the episodes until now.

### **Data modelling with DynamoDB**
I spent a good chunk of days on NoSQL data modelling with DynamoDB using various resources and <a href="https://twitter.com/miksimal/status/1305171665991725059?s=20" target="_blank">applying the lessons</a> to my Virtual Watercooler project.

My favourite resources were:
- <a href="https://www.serverlesschats.com/44/" target="_blank">This episode</a> of Serverless Chats (also a great podcast) with Alex DeBrie.

- Alex DeBrie's <a href="https://youtu.be/DIQVJqiSUkE" target="_blank">re:Invent talk</a>.

- Once I'd watched Alex's talk, I graduated to <a href="https://youtu.be/6yqfmXiZTlM" target="_blank">Rick Houlihan's talk</a>.

- After the talks, I read Alex DeBrie's excellent and well-named book, <a href="https://www.dynamodbbook.com/" target="_blank">*The DynamoDB Book*</a>.

- The <a href="https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/workbench.settingup.html" target="_blank">NoSQL Workbench</a> was an excellent thinking tool when applying the lessons.


### **Best practices and design patterns**

Due to the <a href="https://www.youtube.com/watch?v=BtJAsvJOlhM" target="_blank">dizzying</a> and constantly increasing number of serverless building blocks, having good examples and understanding best practices to combine them into solid microservices within solid overall architectures is essential.

My favourite resources were:

- Jeremy Daly's summary of <a href="https://www.jeremydaly.com/serverless-microservice-patterns-for-aws/" target="_blank">19 serverless Microservice Patterns</a>. Excellent reference. Explains e.g. the 'Frugal Consumer' and 'Scalable Webhook' patterns used in my Virtual Watercooler project to cope with a maximum emails-per-second limit for SES.

- <a href="https://d1.awsstatic.com/whitepapers/architecture/AWS-Serverless-Applications-Lens.pdf" target="_blank">Serverless Application Lens</a>. Quite readable paper from AWS giving detail on various serverless architectures and considerations.

- The intro and linked video in <a href="https://theburningmonk.com/2020/07/how-i-scaled-an-appsync-project-to-200-resolvers/" target="_blank">this article</a> by Yan Cui. Gave me the idea to use Algolia as a 'serverless ElasticSearch' and DynamoDB Streams to trigger a Lambda that synchs changes to it in my Sentimental Robot project.

- These episodes of the 'Real World Serverless' podcast:
  - Episode <a href="https://www.buzzsprout.com/877747/3693316-15-serverless-at-irobot-with-ben-kehoe" target="_blank">15</a> with Ben Kahoe from iRobot.

  - Episode <a href="https://www.buzzsprout.com/877747/3797261-17-findev-and-wardley-mapping-with-aleksandar-simovic-and-slobodan-stojanovic" target="_blank">18</a> (with Aleksandar Simovic and Slobodan Stojanovic) and <a href="https://www.buzzsprout.com/877747/4218644-22-real-world-serverless-with-gojko-adzic" target="_blank">22</a> (with Gojko Adzic) contain good discussion of hexagonal architecture (Ports & Adapters).

### **The business case for 'serviceful serverless'**

Spending so much time on serverless while working in a very 'servermore' (?) environment at work prompted a lot of thinking about this topic. I've got a ton of notes, so will have to write about it soon.

Some great resources are:

- Joe Emison's <a href="https://www.infoq.com/articles/serverless-sea-change/" target="_blank">The Serverless Sea Change</a>. Coining the term 'Serviceful Serverless'.

- These episodes of the 'Real World Serverless' podcast:

  - Episodes <a href="https://www.buzzsprout.com/877747/2870908-2-the-case-for-monorepoes-with-joe-emison" target="_blank">2</a> and <a href="https://www.buzzsprout.com/877747/2871130-3-building-a-fully-serverless-insurance-company-with-joe-emison" target="_blank">3</a> with Joe Emison.
  
  - Episode <a href="https://www.buzzsprout.com/877747/3824681-18-hexagonal-architecture-and-voice-with-aleksandar-simovic-and-slobodan-stojanovic" target="_blank">17</a> with Aleksandar Simovic and Slobodan Stojanovic talking about e.g. 'FinDev' and Wardley Maps.
  
  - Episode <a href="https://www.buzzsprout.com/877747/4615988-24-serverless-at-stedi-with-zack-kanter?play=true" target="_blank">24</a> with Zack Kanter from Stedi.

- Some good discussion about serverless for start-ups between Nader Dabit and Tom McLaughlin in these three threads: <a href="https://twitter.com/dabit3/status/1282002976836550657?s=20" target="_blank">one</a>, <a href="https://twitter.com/tmclaughbos/status/1282028617078386688?s=20" target="_blank">two</a>, <a href="https://twitter.com/tmclaughbos/status/1282084385701998592?s=20" target="_blank">three</a>.

- <a href="https://twitter.com/joeemison/status/1298960701097226240?s=21" target="_blank">This</a> was a great thread to illustrate both (a) a ridiculously small AWS bill and (b) the internet (Alex DeBrie) helping make it even smaller.

- <a href="https://www2.eecs.berkeley.edu/Pubs/TechRpts/2019/EECS-2019-3.html" target="_blank">Cloud Programming Simplified: A Berkeley View on Serverless Computing</a>. 35 page paper with the bold claim that serverless 'represents an evolution that parallels the transition from assembly language to high-level programming languages'.

## Projects
The majority of my learning was structured around the following projects. Whenever I learnt something new, I would go back and apply it to these.

### **<a href="https://virtualwatercooler.xyz/" target="_blank">Virtual Watercooler</a>**
Allows you to create an 'organisation', add members to it, and then randomly pair members for coffee chats - either by clicking a button or by choosing a frequency.

**Backend tech stack:** DynamoDB (single-table design), API Gateway, Cognito, Lambda (Javascript), SQS, SES, Cloudwatch, s3, and CloudFront. All packaged up with Serverless Framework.

Code available <a href="https://github.com/miksimal/virtualwatercooler-backend" target="_blank">here</a>. Wrote <a href="https://dev.to/miksimal/how-to-dynamically-create-cloudwatch-rules-to-let-users-schedule-recurring-actions-2php" target="_blank">this</a> to help me confirm that my approach to letting admins schedule recurring chats made sense.

### **<a href="https://sentimentalrobot.miksimal.com/" target="_blank">Sentimental Robot</a>**
Scrapes BBC news headlines each morning, runs them through sentiment analysis, and allows the user to search through headlines and sentiments, or just get an overview of the past few days' sentiment. Had already started this but built a lot on top during the challenge.

**Backend tech stack:** Algolia, DynamoDB and DynamoDB Streams, Comprehend, CloudWatch, API Gateway, Lambda (Javascript), s3, CloudFront. All except Algolia packaged up with Serverless Framework.

Code available <a href="https://github.com/miksimal/sentimental-robot-backend" target="_blank">here</a>.

### **<a href="https://forgotmyglasses.miksimal.com/" target="_blank">ForgotMyGlasses</a>**
Tend to forget your glasses? No problem, teach the robot what your friends look like and use it to help you recognise them in the wild.

**Backend tech stack:** Rekognition, Lambda (Javascript), Cognito Identity Pool (unauthenticated role), and Cloudwatch. Using Serverless Framework as always.

Code available <a href="https://github.com/miksimal/forgotmyglasses" target="_blank">here</a>.

### **SimpleQuiz (in progress)**
Started this right at the end of the challenge. Decided on the data model and got a basic <a href="https://twitter.com/miksimal/status/1318299480773582849?s=20" target="_blank">real-time connection working with subscriptions</a>.

**Backend tech stack:** AppSync (GraphQL), DynamoDB, Lambda (Javascript), Cognito Identity Pool (unauthenticated role), and a few more probably.

## Lessons for future learning projects

### **Open-ended 'benchmark projects'**
For my learning, I like to define what Scott Young calls <a href="https://www.scotthyoung.com/blog/2019/11/15/drill-or-benchmark/" target="_blank">'benchmark projects'</a>, where you pick something that you cannot do right now, but you _might_ be able to do if you improved your skills, e.g. earning a difficult cloud certification.

This strategy worked well for me for the challenge. Had I tried to define specific topics and learning objectives at the start, I'd have failed as I simply did not have enough of a foundation to do so. The learning objectives I'd have set on Day 0, would have hindered rather than helped me on Day 20.

Had I set a more concrete goal or planned my journey in more detail at the start, for example, I'd never have spent the 30 or so hours on NoSQL data modelling that I enjoyed so much.

Instead, I set the goal of building 2 - 3 relatively 'production-ready' fully serverless projects and let that guide my learning. On day one I started building, and then discovered the missing pieces (such as NoSQL data modelling) I needed to fill in.

I wasn't interested in earning another certification (there aren't any fully serverless ones), but I think that would've been an excellent way to guide learning as well.

### **Learning vs. reporting**

At the start, I stuck diligently to reporting progress and learning every single day. Gradually, I ran into two problems, however. Firstly, as topics got more advanced, I did not always have much to report from a day's worth of learning. Additionally, some days I only had 60 minutes available, so reporting would steal away scarce learning time (with the potential to get distracted on Twitter along the way).

In short, I started having more fun and being more effective once I switched to reporting by progress rather than daily. Sometimes that meant grouping 2 - 3 days, sometimes it was daily. But fitting reporting around the learning rather than the other way around is how I'd approach future projects like this.

### **Becoming 'active on the internet'**
Since I stopped playing World of Warcraft and Counter Strike many years ago, I'd become mostly an 'observer' on the internet.

Seeing the 100 Days of Cloud community grow on Twitter and Discord, frequently reporting progress on Twitter, and following other people's learning challenges was super rewarding and got me back into being 'active on the internet'.

<a href="https://www.swyx.io/learn-in-public/" target="_blank">'Learning in public'</a> like this is extremely powerful, making for better learning, networking, and accountability all in one. For my future projects, I'd need a very good excuse _not_ to build or learn 'in public'.

## Feedback or questions?
I'd love to know if you found this helpful, got any questions I might be able to help with on your cloud journey, or have feedback for me. <a href="https://twitter.com/miksimal" target="_blank">Twitter</a> or <a href="https://www.linkedin.com/in/mikkel-lauritzen/" target="_blank">Linkedin</a> are the best places to connect.
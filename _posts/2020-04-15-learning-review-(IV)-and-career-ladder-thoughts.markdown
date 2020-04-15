---
layout: post
title:  "Learning review (IV) and notes on the software engineering career ladder"
date:   2020-04-15 09:35:00 +0000
categories: learning
---

Since I started learning to code, I have done occassional "learning reviews" where I take stock of what I've learnt and decide what I should learn next (and how). This is the fourth.

My first three reviews along with an explanation of my approach to learning through "benchmark projects" can be found [here](https://mlauritzen.github.io/learning/2020/04/15/learning-reviews-(I,-II,-and-III)-and-benchmark-projects/).

## Learning review, Rd. IV (benchmark almost achieved: become a productive junior dev) + notes on the software engineering career ladder

At my new job, I was given more than 80 hours worth of training (video courses and books) to complete and had to get familiar with a new stack (C#/.NET and Angular).
For that reason, my learning benchmark was simply "become a productive junior dev". This has *almost* been achieved.

I am now:
+ happy working with C# and .NET Core
+ familiar with the key principles of "clean code" such as naming conventions and the SOLID principles,
+ familiar with the design patterns we most frequently use (repository, factory, adapter, e.g.),
+ comfortable with the overall ideas of domain-driven design,
+ comfortable working with Akka.NET actors (almost everything we do in our domains is based on this),
+ comfortable working in both AngularJS and Angular 8/9,
+ written my first unit test for an actor,
+ familiar with CQRS and event sourcing,
+ and, most importantly, I am able to complete basic tasks (with limited guidance) across the stack (I've made minor edits to our third-party API, internal and customer facing websites, and several of our domains and views).

I did a bit of research on role expectations for mid-level / "non-junior" engineers to help guide my learning. I saw these 5 main categories across most careeer ladders:

+ *Independence*: learns quickly and independently; able to prioritise tasks; doesn't get caught up in unimportant details; work only occassionally needs material feedback.

+ *Scope*: able to own clearly defined individual small-medium sized features from technical design through to completion.

+ *Engineering*: understands basic software engineering principles; familiar with industry best practices; understands the system architecture.

+ *Code*: able to write correct and clean code; good sense of "code smells"; mastery of basic language featuers and most advanced structures.

+ *Communication*: able to work well as part of a team; able to prioritise tasks; asks for and gracefully accepts feedback.

The most useful career ladders in this research were:
+ [Basecamp](https://basecamp.com/handbook/appendix-05-titles-for-programmers)
+ [RentTheRunway](https://dresscode.renttherunway.com/blog/ladder)
+ [Fog Creek](https://www.joelonsoftware.com/2009/02/13/fog-creek-professional-ladder/)
+ I also skimmed a few others, but they all roughly fitted into my 5 main themes above. [swyx has a good list of public career ladders](https://www.swyx.io/writing/career-ladders/).

Based on the above, it's clear to me that my main development are is to solidify my knowledge and go from being "familiar" with things to really being fluent.

The best way to consolidate my learning is to write or build, so my next benchmark projects will be:
+ write 3 blog posts summarising my understanding and giving examples of software engineering and clean code fundamentals.
+ build (public on Github!) one project drawing together my learnings (e.g. a project demonstrating concurrency performance benefits with Akka.NET with an Angular frontend).


---
layout: post
title:  "Quality code - and why it matters"
date:   2020-03-22 15:11:00 +0000
categories: learning
---

## Quality code allows you to change your application to suit new requirements

An application built with quality code is easy to change or modify, for example by adding more features.

If you were building an application for a single problem that you knew would definitely stay the same, there'd be 
no point thinking about "quality code" - you should simply get to a solution that works well and move on!

Very few (if any) real world applications are like that, however. Requirements change constantly as customers' needs change
and businesses adapt. Start-ups must constantly iterate on their product.

So, we need quality code!

## But what IS quality code?

We know that quality code is what makes an application easy to modify in the face of new requirements. But what IS it?

I like the following high level definition (from Steve Smith / @ardalis):

> Quality code is
> - easy to understand,
> - easy to change to suit new requirements,
> - easily and quickly tested by automated tests (which reduces the need for expensive manual testing),
> - loosely coupled to infrastructure concerns like databases or files.

## How do you write quality code?
Follow SOLID principles of Object Oriented Design:
- **Single Responsibility Principle:** a class (or, more generally, "a piece of code") should have only one responsibility (or, only one reason to change). I.e. have small, focused classes.
- **Open/Closed Principle:** Open for extension, Closed for modification. I.e. should be able to change behaviour of system, without modifying its source code. For example, add an insurance policy type.
- **Liskov Substitution Principle:** Don't create inheritance hierarchies in which child types are not 100% substitutable for their base types.
- **Interface Segregation Principle:** classes that use interfaces should use all or most of the interface's exposed members -- don't depend on functionality they don't use. Leads to interfaces that are small, focused, and cohesive.
- **Dependency Inversion Principle:** low level concerns should depend on high level concerns, not vice versa. E.g. business layer code shouldn't depend on data access code, but rather an abstraction should exist for the business code to work with which the data access code implements. Ensures loose coupling and more testable code.

And the classic and self-explanatory: **Don't Repeat Yourself (DRY)**!

## "Code smells" imply that your code is not as DRY or SOLID as it could be
"Code smells" suggest that your code is not of a good quality (and probably doesn't follow the above principles). Look out for e.g.:
- code that is difficult to write unit tests for,
- code with lots of comments (ideally you should just be able to read the code like English paragraphs!),
- use of the "new" keyword (suggesting that there's a dependency, which should probably be passed in via the constructor instead).

## Pain-driven development: don't let quality code get in the way!

To ensure all this *increases* productivity, we need to be careful when applying these principles. If we apply them right from the start, we risk ending up spending a lot of time writing very abstract code that does very little.

To combat this, Kent Beck suggests follow these three steps when writing code:
1) First, **make it work**
2) then, **make it right**
3) and finally, **make it fast**.

Steve Smith says something similar, namely to follow ***Pain-Driven Development***. That is, to start out by writing the code you need to solve the problem. *Then*, evaluate whether the code has any major "code smells" (e.g. hard to unit test).

## Useful resources:

* [Pluralsight SOLID course](https://app.pluralsight.com/library/courses/csharp-solid-principles/)
* [This](https://weeklydevtips.com/episodes/047) *Weekly Dev Tips* episode

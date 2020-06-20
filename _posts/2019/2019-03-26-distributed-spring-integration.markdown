---
layout: post
title: 'Distributed Spring Integration '
date: '2019-03-26 16:51:00 -04:00'
author: alberto
categories: Development
tags:
- distributed systems
- spring integration
- spring
- microservices
---

Recently, I was given an opportunity to code a use case that required the need to use EIP in a distributed environment. While trying to use the ```Splitter``` and ```Aggregator``` patterns, I had a chance to review the source code implementation of many of the components used to implement these using Spring Integration.

Highly recommended reading:

* [Introduction to Locks & Leaders](http://presos.dsyer.com/decks/locks-and-leaders.html)
* [Dr. Syer Locks & Leaders Preso](https://github.com/SpringOnePlatform2016/dsyer-locks-and-leaders)
* [How to do distributed Locking](http://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html)

Several points that helped my design implementation using "distributed locks":

* Distributed locks always have a "shelf life" (so it's really a "lease")
* Expiration of a "lock" is essential.
* Use an EIP framework that supports components that remain simple.
* Potential need to move deployments models to a platform environment following a microservices architecture.

So keeping these in mind, Spring Integration fit well. The key objects used were ```LockRegistry```[^1], ```LockRepository```[^2] and ```MessageStore```[^3].

Both XML and Spring POJO Configuration style worked well for managing these via Spring Profiles, and thanks to Spring Boot, keeping these simple was a breeze.

#### References:
[^1]: [LockRegistry API](https://docs.spring.io/spring-integration/api/org/springframework/integration/support/locks/LockRegistry.html)
[^2]: [LockRepository API](https://docs.spring.io/spring-integration/api/org/springframework/integration/jdbc/lock/LockRepository.html)
[^3]: [MessageStore API](https://docs.spring.io/spring-integration/api/org/springframework/integration/store/MessageStore.html)
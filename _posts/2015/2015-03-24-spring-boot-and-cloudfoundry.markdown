---
layout: post
title: Spring Boot and CloudFoundry
date: '2015-03-24T23:20:00.003-04:00'
author: alberto
tags:
- CloudFoundry
- Spring-Boot
- Cloud
- Spring
---

In this post, I'll discuss my experience with Spring-Boot, how its features are making my "rapid prototyping" abilities shine (making me look good) and combined with a nice PaaS such as CloudFoundry, you can finally see how a true "agile" practice can focus on "innovation".

I added most of a sample code for this in a github repo. Feel free to use it and ping me if you need help or have questions:

```https://github.com/albertoaflores/uspto-sample-app```

Coming from a background of Java development, I have been a long  proponent of Spring as an alternative to getting things done quickly. However, even with frameworks like Spring, some configuration tends to be repetitive (e.g. configuring XML/Annotations,  data sources, transactions, controllers, etc) and prone to error. This is where I'm finding great value in the Spring <a href="http://projects.spring.io/spring-boot/" rel="nofollow" target="_blank">Boot</a> project.

As the document suggests, the project is meant to introduce an "opinionated" view of how projects in Spring should be done. That's fine by me since all I care was to get things done and not getting caught up with configuration boilerplate.

## Getting Started
One of the cool features of Spring Boot is that it has a nice <a href="http://start.spring.io/" rel="nofollow" target="_blank">site</a> available to create your project. You can also do everything command line using ```curl```. If you are using STS (SpringSource Tool Suite), this is built in as part of the "New Spring Project > Boot Project" option. Pretty slick!

## Working With Boot
Once you have created your Spring Boot project, the rest is all about creating your classes and some views (javascript and some HTML). Noticed that beans rely on the "classpath" scanner to find your Spring Beans. Furthermore, a number of good practices (both in Spring, Maven, Thymeleaf, etc) are already configured for you. Keep in mind that the "opinionated" nature of Boot is meant to help you focus on the "solving the problem" goal. It does get the job done.

## Customizing your App
The first thing I changed from my Boot App was the banner. Yes, not a big change, but if you are curious this should save you some time. The ```banner.txt``` file can be used to display any banner you'll see in the logs. You can create banners with tools like ```figlet```. I also customized parts of Thymeleaf as well as part of the JPA configuration. The sample code is self explanatory, so I'd let you review it. Other things I changed over time (for some demos) was the backing store from SQL to a MongoDB store (that's not commited to this repo).

## CloudFoundry Deployment
While Spring Boot deploys very well in a traditional Tomcat, it's important to recognize that the app itself is now configured very well to run in a PaaS such as CloudFoundry. In fact, the github project describes this as simple as doing a:

``` cf push ```

The particular github repo contains two projects (each project needs to be deployed in CloudFoundry). One reads data from data.gov and populates it into a database, the other project simply reads from the same database. Both projects are Spring Boot based and are meant to be a sample of not only Spring Boot but some of the features of CloudFoundry.

## Conclusion
I find that Spring Boot does to Spring based applications what Maven does to traditional "ant" style build processes in a clean, and flexible way. The sample code I created took me 2 days to finish (most of the work was in the UI. Notice how many Java classes it has and how much configuration is in there. If you haven't taken Spring Boot a try, give it a shot and make sure to try running it in a hosted CloudFoundry instance such as the one running at <a href="http://run.pivotal.io/" rel="nofollow" target="_blank">http://run.pivotal.io.</a>
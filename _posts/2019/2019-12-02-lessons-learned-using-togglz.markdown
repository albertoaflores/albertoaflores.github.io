---
layout: post
title: Lessons Learned using Togglz
date: '2019-12-02 17:35:00 -05:00'
author: alberto
categories: Development
tags:
- togglz
- spring-Boot
- spring
---

Feature Toggles (a.k.a. Feature Flags) are a common way to test new features in a production environment. I started to experiment with <a href="https://www.togglz.org/documentation/spring-boot-starter.html" target="_blank">Togglz</a> as a OSS library to implement what I needed. For the purpose of my description, I used Spring Boot as it makes apps development simpler. Here are my findings:

First, the documentation says all you need is to add the following:

{% highlight xml linenos %}
  <dependency>
    <groupid>org.togglz</groupid>
    <artifactid>togglz-spring-boot-starter</artifactid>
    <version>2.6.1.Final</version>
  </dependency>
{% endhighlight %}

This is not completely true as the following error occurs:

{% highlight log %}
  [ERROR] contextLoads  Time elapsed: 0 s  <<< ERROR!
  java.lang.NoClassDefFoundError:
  org/springframework/web/servlet/config/annotation/WebMvcConfigurerAdapter
{% endhighlight %}

It appears you need to use the following dependency:

{% highlight xml linenos %}
  <dependency>
    <groupid>org.springframework.boot</groupid>
    <artifactid>spring-boot-starter-web</artifactid>
  </dependency>
{% endhighlight %}

This makes the code compile without problems. Of course, I also need the console module, so I added:

{% highlight xml linenos %}
  <dependency>
    <groupid>org.togglz</groupid>
    <artifactid>togglz-console</artifactid>
    <version>2.6.1.Final</version>
  </dependency>
{% endhighlight %}

This allowed me to have a working app with features enabled/disabled (very quickly I may add). Next was unto setting up a feature flag. This was very easy with the following properties:

{% highlight properties linenos %}
  togglz.console.enabled=true
  togglz.console.path=/toggles
  togglz.console.secured=false
  togglz.console.use-management-port=false
  togglz.features.FAKE_JMS_LOAD.label=Fake JMS Load
  togglz.features.FAKE_JMS_LOAD.enabled=true
{% endhighlight %}

Notice that I had to change the configuration to also not use the management port. This is described <a href="https://github.com/togglz/togglz/issues/203" target="_blank">here</a>.

A few things I would like to see in future distributions:

* Given that Spring Boot is simple to use, I think we should be able to also add a way to add the Owner of a given toggle. This is not possible with the entries.
* In general, Togglz does not have a way to add more description to the flag. This would be super interesting as many features toggles can get lost.

In general, this seems like a good simple implementation of the "Feature Flag" pattern that provides a nice UI to non-technical folks to manage. It's definitely a great start, but I can see having the need to have more features.
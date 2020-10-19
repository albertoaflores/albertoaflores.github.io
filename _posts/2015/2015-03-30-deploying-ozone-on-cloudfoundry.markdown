---
layout: post
title: Deploying Ozone on CloudFoundry
date: '2015-03-30T16:34:00.003-04:00'
author: alberto
categories: development
tags:
- CloudFoundry
- OWF

---

The Ozone Widget Framework (<a href="http://www.ozoneplatform.org/" rel="nofollow" target="_blank">OWF</a>) is a set of tools to enable "widgets" in the UI to communicate to each other. I must admit that the framework (or platform) was an early approach to projects such as "<a href="https://rave.apache.org/index.html" rel="nofollow" target="_blank">Rave</a>" or "<a href="http://wookie.apache.org/" rel="nofollow" target="_blank">Wookie</a>" (Apache), yet I've been asked if CloudFoundry supports it. While my experience using OWF has been somewhat painful, I noticed that an OWF deployment requires a server that is "optimized" for its deployment.  As such, OWF can work on CF using the "buildpack" feature. I suspect you can argue that OWF can be re-written as a web application component to work with the "standalone" java buildpack, however such work is beyond the scope of this post. This post describes what I had to do to create the "ozone-buildpack" to get this working.

If you haven't read the "<a href="http://12factor.net/" rel="nofollow" target="_blank">12 Factor App</a>" site, I recommend you check it and review these principles to adhere when building apps for the cloud. CloudFoundry enables apps that follow these principles. OWF appears to have a fairly "flexible" configuration model to security that breaks some of these principles. In order to preserve this flexibility, I created a basic buildpack for CloudFoundry that enables OWF using Basic Login. Changes to this builpack should enable further configuration to potential OWF deployments, thus preserving some of the flexibility enabled by OWF.

## The Buildpack Model
CloudFoundry uses the buildpack model to deploy applications into a "cloud" environment. This means that all apps deployed will use the same "runtime" as built by the "buildpack". I can not over emphasized how relevant this is. Suddenly, the platform has control over each "runtime" used for a given deployment. For more information on "buildpacks", please refer to the <a href="http://docs.cloudfoundry.org/buildpacks/" rel="nofollow" target="_blank">documentation</a>.

## OWF Dependencies
The official documentation of OWF states that a deployment requires:

* JDK 1.6 or higher.
* Tomcat 7

Upon further reviewing the google groups, you discover that since OWF requires Groovy, you can not use JDK 1.8 yet. Furthermore, I didn't want to try with Tomcat 8, since I read in the groups this hasn't been tested. All of these simply supported the idea of building a "buildpack" for ozone. You can find the repository here:

{% highlight bash noline  %}
  https://github.com/albertoaflores/ozone-buildpack
{% endhighlight %}

## Buildpack Forking
The recommended way to write a custom buildpack is to fork an existing one. As you looked at my repo, you'll find that this code is a fork of the "java" buildpack. The following is a list of the things I had to modify:

### Modified Open JDK to 1.7
This is a change I had to make to the ```config/open_jdk_jre.yml```

{% highlight yaml  %}
---
repository_root: "{default.repository.root}/openjdk/{platform}/{architecture}"
version: 1.7.0_+
memory_sizes:
  metaspace: 64m..
  permgen: 64m..
{% endhighlight %}

### Modify Tomcat 7
This is the change I made to the ```config/tomcat.yml```

{% highlight yaml  %}
---
tomcat:
  version: 7.0.+
  repository_root: "{default.repository.root}/tomcat"
lifecycle_support:
  version: 2.+
  repository_root: "{default.repository.root}/tomcat-lifecycle-support"
{% endhighlight %}


### Implement Appendix C&nbsp; (see Docs)
This is very important! Although it combines a number of files that you probably won't need depending on the deployment configuration of choice. The general principle here is that you can rely in the Tomcat overlay that occurs in the buildpack.

At the end, the sample owf app shipped with OWF deploys without any issues (well, almost none). The code and manifest for it can be found here:

<a href="https://github.com/albertoaflores/owf-app">https://github.com/albertoaflores/owf-app</a>

I'll try to make modifications to this deployment to use Jasig CAS or other implementation. Enjoy!
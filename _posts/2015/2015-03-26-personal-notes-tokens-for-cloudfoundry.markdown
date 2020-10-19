---
layout: post
title: 'Personal Notes: Tokens for the CloudFoundry API'
date: '2015-03-26T06:00:00.000-04:00'
author: alberto
tags:
- BOSH
- CloudFoundry
- REST
---

In using CloudFoundry, I find myself using the CLI more often than not. This works for me very well because I enjoy using CLIs more often than not, however some things can also be done with scripting.

CloudFoundry introduces a REST API available to your installation. This is found <a href="http://apidocs.cloudfoundry.org/" rel="nofollow" target="_blank">here</a>. One of the things you'll notice quickly is that one of the headers has to have an "authorization" token. This can be obtained by running the command:

``` cf oauth-token```

The results can be added to the ```curl``` command as described in the API docs. So that means that something like:

{% highlight bash noline  %}
  curl "https://$DOMAIN_URL/v2/apps" \
     -X GET \
     -H "Authorization: $TOKEN"
{% endhighlight %}

where ```$DOMAIN_URL``` is your CloudFoundry API Endpoint, and ```$TOKEN``` is whatever is returned by the ```cf oauth-token``` command.

Of course, if you simply prefer to make straight calls to the API, you can use the ```cf curl``` command which adds these headers to your HTTP request for free (pending authentication to your given CF instance). So for the example above, you'll have something like this:

{% highlight bash noline  %}
   cf curl /v2/apps
{% endhighlight %}

I'm looking forward to experiment with other CF components shortly such as BOSH.
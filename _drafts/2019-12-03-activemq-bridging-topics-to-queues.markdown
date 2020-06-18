---
layout: post
title: 'ActiveMQ: Bridging Topics to Queues'
date: '2019-12-03T18:51:00.001-05:00'
author: alberto
categories: Development
tags:
- JMS
- Messaging
- ActiveMQ
---

Most recently, I had the need to create a bridge from Topics to Queues to create stateless services that can pick up messages in parallel. Essentially, I wanted to configure the following (in the message broker):<br /><br /><a href="https://1.bp.blogspot.com/-ltkvc-YBtZk/XebwSWwWeAI/AAAAAAAAYTg/6fIGIguE6XU6pOxSr2MEf3CAcsRfAepEACLcBGAsYHQ/s1600/Topic-Queue-Bridge.jpg" imageanchor="1" style="margin-left: auto; margin-right: auto;"><img border="0" data-original-height="164" data-original-width="319" src="https://1.bp.blogspot.com/-ltkvc-YBtZk/XebwSWwWeAI/AAAAAAAAYTg/6fIGIguE6XU6pOxSr2MEf3CAcsRfAepEACLcBGAsYHQ/s1600/Topic-Queue-Bridge.jpg" /></a>



While there are many other ways to do this, I wanted to experiment with ActiveMQ support for this. The following is how I configured it locally (in my dev box):<br /><br /><a name='more'></a><b>Use a Docker Image</b><br />I used an ActiveMQ docker image found <a href="https://hub.docker.com/r/rmohr/activemq" target="_blank">here</a>. It was pretty straightforward and was able to get it running after a few commands. Here is what I did to define a baseline (this is from the instructions in the link above):<br /><pre>  <code class="shell">docker run --user root --rm -ti \<br />  -v /Users/alberto/workspace/docker/activemq/conf:/mnt/conf \<br />  -v /Users/alberto/workspace/docker/activemq/data:/mnt/data \<br />  rmohr/activemq:5.15.4-alpine /bin/sh<br /></code><br /></pre>Notice the following:<br /><br /><ul><li>I created the /conf and /data directory in my dev box.</li><li>I mounted these folders into the /mnt/* respective to my local box.</li><li>As the end of this command, a shell will be started inside the docker container</li></ul>Then, I had to do the following (within the docker container): <br /><pre>  <code class="shell">chown activemq:activemq /mnt/conf<br />chown activemq:activemq /mnt/data<br />cp -a /opt/activemq/conf/* /mnt/conf/<br />cp -a /opt/activemq/data/* /mnt/data/<br />exit<br /></code><br /></pre>Now, I have the configuration in my "conf" folder.<br /><br /><b>Configure ActiveMQ</b><br />Within the "conf" folder, we need to edit the activemq.xml file.<br /><script src="https://gist.github.com/albertoaflores/40e6001df626f65aca561672cb3200fd.js"></script><b><br /></b>The important lines here are from 125 to 136 where I use "VirtualDestinations".<br /><br /><b>Test Message Forward</b><br />You can now go to the admin console at:<br /><br />&nbsp;&nbsp;<a href="http://localhost:8161/admin/send.jsp">http://localhost:8161/admin/send.jsp</a><br /><br />and send a message to the topic. You will see messages forwarded to the queues of your choice.<br /><br />
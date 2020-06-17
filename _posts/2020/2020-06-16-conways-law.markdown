---
layout: post
title:  "Conway's Law"
author: alberto
date:   2020-06-16 10:20:32 -0400
categories: transformation
excerpt: Digital transformation is not just about the tech. It's about people, process and tools (in that order). As many industries continue their transformation journey, some core principles are arising. In 1967, Melvin Conway introduce a concept that is now known as "Conway's Law". It is very commonly used to describe how systems are designed and how teams are limited by different factors.  In this post, we describe some of these.
---
Software development is both an "art" and a "science". One has to recognize when both are needed. Too much "art", and you miss the "engineering" piece of it. Too much science, and you lose the intrinsic elements of the experience, such as "culture" and "outcome focus". In fact, the so call "Digital Transformation" wave is all about finding a balance between these two. One of the elements of the intersection of "art" and "science" is explained in Conway's law:

> "Any organization that designs a system will inevitably produce a design whose structure is a copy of the organization's communication structure." [^1]

## It's a People, Process, and Tools Problem
 It's interesting to think that this is not a new problem. Distributed systems have been dealing with Conway for a very long time. It's important to recognize that many are moving to a "Micro-services architecture" while not neccesarily realizing the implications of building a "distributed system".

 It follows then that the impact of Conway's Law will be felt in not just our system design, but also in our culture, and process used throughout the organization. Furthermore, Conway suggests the need of organizational design at the team level coupled with a process that focuses on a value stream. Interestingly, this means that it is equally important to focus on the organizational structure of your team, just as much as your process and tooling.

## Tackling the Culture
Building complex system is never done in a culture of "heroes". This is simply a math problem: The pool of heroes exists, and while very useful in a "start-up", scaling such teams can prove to be very expensive in the long term as enterprises create "Dungeon Masters" [^2]

Everyone can make a reference to Agile and/or Lean development, but very few speak on the doing "Agile at Scale". I have found great inspiration in how the Spotify folks have done this. I highly recommend watching both [^3] videos [^4]. This can only be done with proper alignment (direction). What the Spotify folks have done is great food for thought, but it's not meant to be a blue print. Organizations need to define the structure that creates the right value while keeping the negative impact of Conway's Law at a minimum.

## Little's Law: it's all about productivity
If Conway helps us with the organization structure from a high level, we still need to solve the problem of what each team does and how fast they are able to deliver (or not deliver) value. Cross-functional team members are meant to solve the "time to market" problem: Be autonomous, but don't sub-optimize.

As also discussed in Hackernoon [^5], John Little's mathematical proof gives us further insight:

$$ Average Lead Time = \frac{ Average Work in Progress}{Average Throughput}$$

In this context, "Lead Time" is the time for things to get done. Little's law helps us measure how the amount of time it takes to complete tasks (e.g. stories, features, etc) is directly proportional to the number of "things" we are working on. One can only conclude that for teams to get done faster, they need to commit to work on fewer things. This suggests an intrinsic need to prioritize "acceptance" criterias to determine MTP (Minimum Testable Product) so that we can start to learn quickly.

## What about the Tools?
One of my favorite quotes from Steve Jobs is:

> "It doesn't make sense to hire smart people and tell them what to do; we hire smart people so they can tell us what to do".

Tools will most likely be needed to design and implement solutions. While we need to codify how to best use these (e.g. handbook of instructions), this is where we allow innovation to happen. Tools will arise as part of the solution, hence we don't start with these enforcement. In my experience, teams need a lab to experiment. The need to productize these tools is in part why an "opinionanted platform" is critical for the sucess of an enterprise.


#### References:
[^1]: [{{ site.data.bookmarks['conwayWikipedia'].title}}]({{site.data.bookmarks['conwayWikipedia'].url}})
[^2]: [{{ site.data.bookmarks['dungeonMasterAntipattern'].title}}]({{site.data.bookmarks['dungeonMasterAntipattern'].url}})
[^3]: [{{ site.data.bookmarks['spotifyEngineringCultureVideo1'].title}}]({{site.data.bookmarks['spotifyEngineringCultureVideo1'].url}})
[^4]: [{{ site.data.bookmarks['spotifyEngineringCultureVideo2'].title}}]({{site.data.bookmarks['spotifyEngineringCultureVideo2'].url}})
[^5]: [{{ site.data.bookmarks['conwayAndLittle'].title}}]({{site.data.bookmarks['conwayAndLittle'].url}})
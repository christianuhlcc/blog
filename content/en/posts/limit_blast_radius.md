---
title: "Operational Excellence: Limit Blast Radius"
date: 2023-01-05T10:35:00+01:00
draft: true
featured_image: "/images/blast.webp"
tags: [Operational Excellence]
---

Trying to prevent all failures is a foolish endeavor. This doesn't mean you're not supposed to prevent and reduce failures as much as you can, but limiting the impact of failures turned out to be the most impactful strategy I found around Operational Excellence so far. In this article, we'll explore some strategies to limit the pain of outages in your software system.

{{< figure src="/blog/images/blast.webp" attr="Photo by [Julius Drost](https://unsplash.com/@juliusdrost)" alt="Old chair in front of an abandoned and decaying wall ">}}

> This article is the first part of a series around [_operational excellence_](/blog/tags/operational-excellence/), you can follow the tag for related articles after I posted more.

The metaphor of "blast radius" describes how _far_ a problem in your system travels. In poorly resilient distributed systems, failures propagate and take usually the whole thing down with it.[^1] 

> A distributed system is one in which the failure of a computer you didn't even know existed can render your own computer unusable -- Leslie Lamport


## Make your outages partial
### Separate Frontend and Backend

### Modularise your Frontend

### Resiliency Patterns between Services



## Limit affected users

## Reduce Downtime

[^1]: https://web.archive.org/web/20171107014323/http://blog.fogcreek.com/eight-fallacies-of-distributed-computing-tech-talk/
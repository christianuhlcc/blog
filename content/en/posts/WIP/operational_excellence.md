---
title: "Operational Excellence for the rest of us"
date: 2022-12-14T10:35:00+01:00
draft: true
toc: true
---

‘We have a "You build it you run it" approach here.‘, your boss gleefully tells you. Then she gives you the access keys to your cloud provider and marches out of the office, while you and your team start building right away. A few months later, you find yourself in a tribunal with her, your CEO and a few angry big-shot customers. They are screaming about "too many outages" and it looks like they try to burn you alive in the meeting room. Does this story sound familiar? 

## What is operational excellence?

When I use this term, I try to describe a system where Technology, Processes and Culture are tuned together to operate and maintain a complex software system in a way that becomes highly available and provides correct data and a full feature set [^1]. 

Such a system is maintained by an organization that 
* Uses raw technology (e.g. building blocks from the resilience toolkit like circuit breakers, retries with exponential backoffs, fallbacks and graceful degradation) 
* Has processes in place to discover and learn from problems, and funnel these learnings back into the system (Like blameless post-mortems, chaos engineering and architecture reviews)
* Has a culture that cares about this and enables people to leverage both technology and processes enough to make a meaningful difference (Maybe by providing operations SLOs in their ORKs, or by promoting people who have impact on operational stability)

# Excellence doesn't come for free

The bar for cloud software is pretty high nowadays. The large players in the industry figured out how to keep insanely complicated software stacks available (almost) 24/7, and surprisingly bug-free. Sure, things could always run better and faster, but overall the web is a pretty pleasant experience if you understand the complexity behind it. And of course, rightfully so, our customers and stakeholders expect similar professionalism from our little donut shop where we happen to work (Even if that Venture Capital funded donut shop is valued at 10B$). And since the big players were kind enough to open-source most of their tooling, we have a lot in our arsenal to build resilient systems.

Unfortunately, the reality is often different: Outages, downtimes and latency spikes are a sad reality of many systems.

As with pretty much everything in life, you will initially suck at operating your software stack. You can either get better the hard way, by grinding it out and burning through a lot of people, or by skipping a few steps and learning from the others who failed before you. In this post, I'll try to collect my learnings over the years so far on how to actually improve availability and general impression of the quality of your complex application.

> ***Disclaimer***: As any article, to paraphrase [Cindy Sridharan](https://twitter.com/copyconstruct), this advice is aspirational in nature. I am quite aware that there are a ton of things we still have to figure out at Personio to achieve a better user experience in our rapidly growing system. If you have additional ideas besides the ideas here, I would love to hear about them.

## It starts with awareness that this is a problem and needs fixin'

As a stakeholder, CEO or any other non-technical person, you would rightfully assume that the software your highly-paid engineers build would just work well all the time. Same as when you let an architect construct a house, you expect it to at least not collapse in the first century after building.

In software, complexity grows superlinear with the amount of engineers that are working on it and the amount of functionality it contains. To keep the system stable, your impact toward operational excellence must match the amount of complexity introduced in the same period.

This means operational excellence for your software system is a deliberate, and costly effort that has to be undertaken to get anywhere. You have to do things, not just require the system to be "good".

## Measure your status quo and set ambitious goals

It's not a matter of feelings of how well system runs, you should have clear numbers that measure how well things are going.


### Synthetic Tests

Especially for multi-tenant SAAS systems, I found [synthetic tests](https://www.datadoghq.com/knowledge-center/synthetic-testing/) to be very valuable: A bot executes a few important flows in your system periodically and measures how often it is successful as well as performance metrics. This technology has similar downsides as End-to-End tests (flakiness, brittleness against changes, needs cleanup of created data artifacts), but still gives you a neat constant measurement of your key user journeys. It's a lot better than simple uptime monitoring but more costly to implement and maintain.

### Observability



### Have SLAs with your customers, and stricter internal SLOs

## Improve the status quo

So now you know we have a problem on our hands, how do we go on about fixing it?

--- see this post on post mortems ---

### Architect your system to limit the blast radius of problems

### Build a culture that cares

If you have frequent outages and post-mortems (Ouch! I know that pain): Run a regular meeting with top-level leadership (at least your CTO/VPE and similar representatives from Product and Customer Experience) to discuss them collectively. If its even worse, you can even have sub-meetings for smaller org units and aggregate up. You can discuss outages on a meta-level, and make sure Action items and learnings get put into action promptly. If you feel it's appropriate you can make this meeting blameful and make sure people have to stand for the quality of their subsystems - Not to blame individual actions that caused problems (if there was nothing malicious), but to blame a lack of improvement.




## Protect a healthy state

The sad news is that you will never be really done with this, as complexity or scale of your application grows you will face new exciting problems. But the good news is once you have injected operational excellence into your culture, it can self-propel forward and new solutions will emerge as soon you need them. As leaders, our job is to protect the space for this work and keep advocating and holding people accountable.

[^1]: Of course within the limits of how distributed systems can act: https://arxiv.org/abs/1509.05393
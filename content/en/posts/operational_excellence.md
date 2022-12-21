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

### Learn from your Failures via blameless post-mortems

True Blameless Post-Mortems are a work of art, but once you get them right habitually they become a powerful tool for improvement and learning. This might be a full-featured blog post later on just to dig into post-mortems. The core idea is that when a problem occurs, it was not the fault of the human who did the wrong thing - it was the fault of the system for allowing the action to happen. 

As a simple example, if your intern manages to delete the production database, that's not the fault of the intern. That's the fault of your setup for giving them the right to run `DROP DATABASE` on prod in the first place.

In a nutshell, a post-mortem investigation happens after the problem, where you create a document with the rough following content:

* What exactly went wrong:
Describe the problem in understandable words, for easier aggregation and discoverability. This should also contain the impact of the problem, and lots of metadata for classification and analytics. How many customers were impacted? What data was lost? How many requests failed? What was the p99 latency of requests during the time?
* The cause of the error:
The word root cause has fallen a bit out of fashion, as the true root cause for most failures is something you can't do much about, like ... captialism. But you also can't stop at the surface of the problem either. Using the 5-Why technique can be helpful here
* The actions forward:
There should be clear and actionable items as the outcome of the post-mortem analysis. They need a clearly assigned owner who is accountable for bringing the action item to the team and clearing it.

If you can, automatically collecting the action items to have an overview page about what's still open was very helpful for us, to make sure we cover enough ground. A really bad signal is when you have two outages


But what I find very hard about post-mortems is that it's ***hard*** to write good action items, and few people can teach you how to do that. If you throw a random set of engineers into a post-mortem meeting, chances are your action items will just prevent the very exact problem from happening again in the exact same circumstances, or they will propose the grad refactoring of your stack that you won't do ever. "Rewrite it in Rust" is a joke, not a good action item.

#### Roles in the post-mortem meeting

But how do you get good at them? I think a good post-mortem meeting has two dedicated roles that should be present in addition to the relevant engineers for the problem:

1. Moderator

I used to do this role a lot - Discussions are easy to run too deep, and you 
might optimize too much on describing or researching the topic. Somebody who doesn't have to contribute can focus on typing, screen sharing and timekeeping. I admit it's sometimes hard not to dive into tech myself, but I always had great peers who could do that job better than I could have.

2. Advisor / Bar Raiser

Somebody who knows what a good post-mortem looks like, and can hold the group accountable for high-quality analysis. I believe that during writing, it's a lot easier to add constructive criticism than afterward. We have a "critique" aspect when we presented the post-mortem to the whole engineering group, but it feels unconstructive and blame-y. I would love to introduce that role to our post-mortems, to improve quality without making people defensive. This _can_ be done by the moderator, but I wasn't particularly good at that.


#### Additional tips I found useful for good post-mortems:

* Start the document right away during the outage, and post raw data, links and screenshots there as soon as you have them, it will be a lot easier than searching for it later, and it helps to onboard late joiners to the discussion. Which also means you should use a collaborative editor like google docs or confluence.
* Use screenshots where possible as many references (logs, your APM system) might get cleaned up after a while and that data is gone. Pictures of charts are always useful.
* Prepare and tighten the document before the synchronous meeting, so that you don't waste time struggling with your editor and can focus on the content instead. Most of the investigation about what went wrong and what was impacted can be researched by one person beforehand. The post-mortem meeting should focus on the way forward, and how to make your system more resilient. That's where the value lies, and where you need the collective creativity and discussion of the group.
Scrutinize the action items as much as possible, this is where you need to 
* Present the post-mortems to the whole engineering body - Don't expect that all lessons stick, but I remember a few post-mortems being referenced in my teams that they didn't run themselves. Knowledge spreads and sometimes prevents things you have no automated guardrails against.

### Architect your system to limit the blast radius of problems

### Build a culture that cares

If you have frequent outages and post-mortems (Ouch! I know that pain): Run a regular meeting with top-level leadership (at least your CTO/VPE and similar representatives from Product and Customer Experience) to discuss them collectively. If its even worse, you can even have sub-meetings for smaller org units and aggregate up. You can discuss outages on a meta-level, and make sure Action items and learnings get put into action promptly. If you feel it's appropriate you can make this meeting blameful and make sure people have to stand for the quality of their subsystems - Not to blame individual actions that caused problems (if there was nothing malicious), but to blame a lack of improvement.




## Protect a healthy state

The sad news is that you will never be really done with this, as complexity or scale of your application grows you will face new exciting problems. But the good news is once you have injected operational excellence into your culture, it can self-propel forward and new solutions will emerge as soon you need them. As leaders, our job is to protect the space for this work and keep advocating and holding people accountable.

[^1]: Of course within the limits of how distributed systems can act: https://arxiv.org/abs/1509.05393
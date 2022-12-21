---
title: "Operational Excellence: Learning from failure"
date: 2022-12-21T10:35:00+01:00
draft: false
featured_image: "/images/fail.webp"
tags: [Operational Excellence]
---

Failure is inevitable. But every failure is an opportunity to learn, and to harden your system against more catastrophic failures later down the road. Blameless post-mortems are a very good tool to achieve this and have been adopted quite widely in the industry already. But of course the details and diligence of this process varies a lot, so I've taken a stab at putting together all I know about how post-mortems can be great.

{{< figure src="/blog/images/fail.webp" attr="Photo by [Ian Kim](https://unsplash.com/@hewittlv)" alt="picture of a wall with a neon sign saying -people fail forward to success-">}}

> This article is the first part of a series around [_operational excellence_](/blog/tags/operational-excellence/), you can follow the tag for related articles after I posted more.

# Learn from your Failures via blameless post-mortems

True Blameless Post-Mortems are a work of art, but once you get them right and a habit, they become a powerful tool for improvement and learning.  The core idea is that when a problem occurs, it was not the fault of the human who did the wrong thing - it was the fault of the system for allowing the action to happen. 

Let's remind ourselves on why they have to be blameless: As soon as you assign blame to individuals, they will go into damage control mode, and insights will be hidden - probably the whole investigation will be avoided in the first place. It will feel good to smack someone's hands for a problem, but the systemic problem will still be there, and you'll inevitably face the same problem again.

As a simple example, if your intern manages to delete the production database, that's not the fault of the intern. That's the fault of your setup for giving them the right to run `DROP DATABASE` on prod in the first place. If you fire the intern or not won't matter - the next intern next year might do the absolute same again. So you must work on the permission system instead.

In a nutshell, a post-mortem investigation happens after the problem, where you create a ***document*** with the rough following content:

* ***What*** exactly went wrong:
Describe the problem in understandable words, for easier aggregation and discoverability. This should also contain the impact of the problem, and lots of metadata for classification and analytics. A timeline of actions and evidences helps a lot, starting with maybe a faulty commit or observed behavior.
* The ***impact*** of the problem:
To understand the severity, you need to understand how many of your customers were impacted in what way.  How many customers were impacted? What data was lost? How many requests failed? What was the p99 latency of requests during the time? If you treat every problem with the same panic brush, people will rapidly get tired of your process, and you'll lose out on valuable learnings.
* The ***cause*** of the error:
The word root cause has fallen a bit out of fashion, as the true root cause for most failures is something you can't do much about, like ... capitalism. But you also can't stop at the surface of the problem either. Using the 5-Why technique can be helpful here to dive just deep enough to make reasonable changes, without having to overthrow your government first (That wouldn't fit into a two-week sprint)
* The ***actions*** forward:
Here's the critical part: There must be a small amount of clear and actionable items as the outcome of the post-mortem analysis. The goal of these items is that after completion, a _similar_ situation or action will not lead to a problematic state again. The system will be hardened.

If you can, automatically collecting the action items to have an overview page about what's still open was very helpful for us, to make sure we cover enough ground working on our learnings. A really bad signal is when you have two outages where the second would have been prevented by the learnings and action items from the first.

## Good action items

But what I find very hard about post-mortems is that it's ***hard*** to write good action items, and few people can teach you how to do that. If you throw a random set of engineers into a post-mortem meeting, chances are your action items will just prevent the _very_ exact problem from happening again in identical circumstances, or they will propose the grand refactoring of your stack that you won't do ever. "Rewrite it in Rust" is a joke, not a good action item. That's why I propose to have an advisor/bar raiser as a dedicated role in post-mortem meetings.

Of course, things that are habitual by nature are also terrible action items. An item like "be careful next time" will be quickly forgotten when the next deadline rolls around, so delete them or put the "learnings" into a separate bucket.

I would advise having a general rule in place of how big action items can be (For example, it should be doable in the next two weeks), but allowing the Engineering Manager or similar leader to grant an exception for bigger pieces of work if they are necessary. Of course, that would make them accountable for pushing that larger item then through. Good rules need the option to override them if reality gives you a good reason.

What I know is useful is that they need exactly one assigned owner who is accountable for bringing the action item to the right team and clearing it.

## Timeliness of action items

This is admittedly something where I haven't found the golden path yet, but I am trying to give it my best shot:

It doesn't matter how good your action items are if you never get around to doing them. So it's an organizational habit to give priority to post-mortem action items - usually the same level as critical bugs. If you have a "dedicated person" in your team (Sometimes called Firefighter, Hero, Maintenance Person, or more generally "Victim"), it should be on their stack.

## Roles in the post-mortem meeting

But how do you get good at them? I think a good post-mortem meeting has two dedicated roles that should be present in addition to the relevant engineers for the problem:

1. Moderator

I used to do this role a lot - Discussions are easy to run too deep, and you 
might optimize too much on describing or researching the topic. Somebody who doesn't have to contribute can focus on typing, screen sharing and timekeeping. I admit it's sometimes hard not to dive into tech myself, but I always had great peers who could do that job better than I could have.

2. Advisor / Bar Raiser

Somebody who knows what a good post-mortem looks like, and can hold the group accountable for high-quality analysis. I believe that during writing, it's a lot easier to add constructive criticism than afterward. We have a "critique" aspect when we presented the post-mortem to the whole engineering group, but it feels unconstructive and blame-y. I would love to introduce that role to our post-mortems, to improve quality without making people defensive. This _can_ be done by the moderator, but I wasn't particularly good at that. 

## Running post-mortems at scale

Another support structure that can work well is to have an aggregate format (like an operational excellnce forum) in your org units, where team leaders participate. These meetings can be blameful, and should focus on:
* Timeliness execution of action items and learnings
* Process improvements based on aggregate learnings from many post-mortems
* Enforces a high-quality bar of post-mortems

## Understanding the Severity of Outages, and when to run the post-mortem process

While the post-mortem process is helpful, and it's always great to learn where you can, a good post-mortem process is also expensive. Additionally, there's a natural tendency to hold leaders accountable for the raw number of incidents in their groups, which incentivizes them to not classify things as "needs a post-mortem".

You can avoid unproductive discussions during an outage by having a clear taxonomy of problems. For example you could group things into Severity classes:

* ***Sev 1:*** All of production is down, no customer can access anything, data loss happens or you have a security incident.
* ***Sev 2:*** A major flow or functionality is impacted for all customers or performance has significantly degraded.
* ***Sev 3:*** A group of customers can't access some functionality, for others, it's still working.
* ***Sev 4:*** Internal tooling is not working as expected.

This will also allow you to see a trajectory of how your architecture evolves - If the share of SEV1s goes down, and the amount of outages stays constant, you are getting better at limiting the blast radius of your changes and decoupling systems better.

I would also add a section for "Security Incidents" in your post-mortem template to make sure that the security dimension, if appropriate, is looked at correctly.

## Add Mandatory fields and insights to learn at scale

I would suggest having (and enforcing) machine-parsable metrics in your document template so that you can run analyses on your history of outages. 

Good examples would be 
* MTTR (Mean time to recovery)
* MTTD (Mean time to detect),
* Origin of fault (code change, infrastructure failure, external dependency failure)
* Type of resolution (rollback, fix forward, scaling infrastructure)
* Detection (autodetected, internally noticed or noticed by the customer first?) 

I remember the effort I had when I made a spreadsheet analysis of post-mortems to advocate for canary releases (which we ultimately did), and that was before we had these metrics in the template. Now it would be way easier to get the same insight. The same goes for a chart that shows the development of MTTR over time, to track if you're improving. Thanks, [Martin](https://www.linkedin.com/in/martin-lechner-01b99056/) for the suggestion!

## Additional tips I found useful for good post-mortems:

* Start the document right away during the outage, and post raw data, links and screenshots there as soon as you have them, it will be a lot easier than searching for it later, and it helps to onboard late joiners to the discussion. This also means you should use a collaborative editor like google docs or confluence.
* Have a good template for post-mortems to scale it out with less experience needed, but still train your moderators.
* Use screenshots where possible as many references (logs, your APM system) might get cleaned up after a while and that data is gone. Pictures of charts are always useful.
* Prepare and tighten the document before the synchronous meeting, so that you don't waste time struggling with your editor and can focus on the content instead. Most of the investigation about what went wrong and what was impacted can be researched by one person beforehand. The post-mortem meeting should focus on the way forward, and how to make your system more resilient. That's where the value lies, and where you need the collective creativity and discussion of the group. A temporary chat channel works well for this, and it's the responsibility of the moderator to keep the discussion flowing here
Scrutinize the action items as much as possible, this is where you need to 
* Present the post-mortems to the whole engineering group - Don't expect that all lessons stick, but I remember a few post-mortems being referenced in my teams that they didn't run themselves. Knowledge spreads and sometimes prevents things you have no automated guardrails against.



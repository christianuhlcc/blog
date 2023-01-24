---
title: "Navigating the economic downturn as an Engineering Manager"
date: 2023-01-21T13:35:00+01:00
draft: false
featured_image: "/images/downturn.webp"
images: ["images/preview/downturn.jpg"]
toc: true
---

We are right in the middle of a pretty serious economic downturn: We see big layoffs at major tech companies, the stock market is on fire and all companies are switching gears. I collected some thoughts on how Engineering Managers can best navigate this downturn and adapt what we've been doing during the boom years. Let's explore good ways on how to do more with less, how to support our teams during this cycle and how we could adapt our hiring for the time to come.

{{< figure src="/blog/images/downturn.webp" attr="Photo by [CHUTTERSNAP](https://unsplash.com/de/@chuttersnap)" alt="Broken ceramic">}}

## Do more with less

When I first heard the term "do more with less" I found it quite confusing: What am I supposed to do with that? - I am pretty sure that I have always tried to keep "bloat" away from my teams as much as I could during the good times. So what would be now to cut? And if there was anything I could cut, shouldn't I have cut it long ago? But a changed situation changes also the lens through which we perceive reality. We can use this as a good checkpoint to reassess our strategy for the team and improve our chances for future funding. 

### Focus on doing the "right things"

Sundar Pichai just recently said "Scarcity breeds clarity.": In times of plenty, you could run a lot of experiments and big bets. Things that might become wildly useful - and when times get tight, that's no longer the case. I would suggest evaluating all projects you are doing under one dimension:

***Will this initiative contribute to the company's bottom line this financial year?***
 
And if not, work hard to cut them, postpone them or reduce your engagement. Your Product Manager is again your best friend in this situation, make sure you work closely together to find the right opportunities. You very much want your team to be on the positive side of the spreadsheet when the next round of budget reduction rolls around. If you have no topic, I would strongly suggest pausing some of your current work and supporting other teams that have such a thing. 

Maybe it's also time to ship things "dirtier" or more incrementally than you used to do - not completely neglecting quality, but expressing some sense of urgency upwards will reflect positively on your team. Carefully taking on tech debt where it makes sense (and is known to everyone) can be useful.

### Look at your spending

On the counter side of speed, it might be a good time to look at your spending: While it was a good tradeoff last year to "throw hardware at problems" when it allowed you to ship faster, I would suggest thinking more diligently about cloud or hardware costs for the product you are building. It's probably more helpful to fix some overprovisioning problems before somebody comes after your team event and education budget.

### Build psychological safety 

No team can ship at high velocity if they don't feel safe[^1]. And in turbulent times, it's likely that they don't feel as safe as they used to. I put a whole section in later for this topic, but I want to highlight that "do more with less" will only work if the mental state of your teams is healthy.

### Spread Knowledge

The smaller teams become, the more critical islands of knowledge get. My highest-performing teams were always those where everyone could work on every corner of the product, and work could swing in any direction we needed. If you can see that your work iteration needs to be fluffed up so that everyone has something to do, instead of all working on the most important thing, you know where to start.[^2] Beware that it might happen that some of your high performers get reassigned to other projects, and your team must not stall completely when that happens.

### Fight bikeshedding

Besides the aforementioned psychological safety, this does not mean that your team should be unaware of the seriousness of the situation around you. To also drive home the point, you can try to cut down on [bikeshedding](http://phk.freebsd.dk/sagas/bikeshed/) wherever you see it - endless discussions about trivial technical matters that ultimately won't make any difference.

## Be there for your team

A lot of people will adjust a lot of processes and rules now in your organization, and poor change management will hit left and right. Now combine that with the ever-growing uncertainty, and some of your team members might be mentally holding on for dear life. You are a leader, be there for them and keep explaining what's happening. Make sure they can understand and put the latest organizational changes in the proper context. Go do extra loops in your 1:1s and dig into that topic. I can recommend [this collection of ideas](https://larahogan.me/resources/resilience/) from Lara Hogan

You might feel uneasy yourself, but your team is not the place to discuss this - use your peers and support network for your own worries, and be sure to radiate all the (appropriate) confidence and positivity you can muster up. But also make sure you have your own "oxygen mask" on first and are taking care of your own emotional well-being - otherwise, you won't be able to help your team.

You might also have some people reporting to you who are experiencing their first crisis and might have known only the great bull run of the last 5 years as their employment reality. They are in for a rude awakening, and you should support them during that realization. For them, it's a new concept that organizations are at the end of the day capitalistic and uncaring entities that will fire you the very second you are on the wrong side of a spreadsheet - and that's a terrible realization if you have been blinded by employer branding your whole career. We as leaders, given our average tenure in the workforce, have likely seen this ugly side before. Don't look down on your youngsters for freaking out about this, support them through it. We have been there before, it's just a long time ago.

## Adapt your Hiring

Times are getting tight for us hiring managers. After the insane hiring rush of 2021 and 2022, when Headcount was plenty and applicants were rare, we see a massive shift towards "doing more with less". How will this affect the roles and people we will hire for the next year?

### The senior trap

It's an easy one to fall into - if you can staff only 3 of your previously thought 12 positions you might be incentivized to get as-senior-as-possible candidates. The same goes for when you have a promising senior candidate in the pipeline, and you have a mid-level opening planned in your team. Easy win right? More senior is better? You get more bang for your buck (headcount position) of course.

Unfortunately, this is - as many easy answers - not the full truth. Having dis-balanced teams with too many seniors leads to pretty icky problems later on:

* Seniors are usually more effective at solving larger, more complex problems. Unfortunately, if there are not enough large problems to solve, Seniors tend to create large problems to then solve them: 

> "Our architecture was fairly good and effective until the Staff engineers decided that they need to have more impact"

* Having too many Seniors on the team is a challenge for the “regular” work that we need to do. I think a good metaphor is “You need someone on the team who is excited about adding a button” - and more junior people are excited about that. Every project has a fair amount of that work, and it's better to have people that are excited about this.

* We all grow a bit more cynical as we go through our careers, ending somewhere between realism and pessimim. Every team needs a bit of young blood, people who believe that it might actually work what you're trying to do. A bit of reality distortion or hopeless optimism can move mountains.

{{< tweet user="shanselman" id="1617239827874992128" >}}

* With an unbalanced team, the Seniors are not able to mentor others, which hinders their career progression. Even worse, they might start trying to mentor each other without consent and get up in each other's faces, harming the team's mood. 

### Up the quality bar

I did up to 10 interviews per week for a while and it drove me slightly insane. It might be tempting after the hiring insanity to slow down on interviewing, as there are fewer slots to fill, right? Well, I am here to foil your plans - I believe that during times of crisis, you will see a lot of people on the market that you usually won't have access to: Some truly great people get hit by random layoffs, and they are usually hired within their network. Only when things get disturbed is when these people hit the regular hiring market. So if you can, readjust some of your hiring time towards raising your hiring bar, and doing active outreach. You can use tools like [layoffs.fyi](https://layoffs.fyi/) to get access to profiles. Make sure people are aware that your company is still hiring :-)


[^1]: You can start with this [meta-study](https://www.sciencedirect.com/science/article/pii/S1053482217300013) about psychological safety or the original [re-work article](https://rework.withgoogle.com/blog/five-keys-to-a-successful-google-team/)

[^2]: Of course that will be hard to fix, and should have been fixed during the good times, but as the saying goes "The best time to plant a tree was 20 years ago, the second best time is now"
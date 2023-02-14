---
title: "Splitting teams"
date: 2023-02-01T10:35:00+01:00
draft: false
toc: true
featured_image: "/images/split.webp"
images: ["images/preview/split.jpg"]
tags: [Hypergrowth]
---

When I need to grow my engineering organization, I often prefer growing and splitting teams over bootstrapping completely new teams. Even though growing teams is slower than just bootstrapping on the green field, I still go for it as you can spread and transfer the most domain and tribal knowledge into both new teams, and keep your existing culture largely constant. During the hypergrowth of Personio, I was fortunate enough to participate in multiple teamsplit events, and I collected my learnings and what went well in this article. 

One important caveat in hypergrowth is that the split approach scales until approximately doubling your organization year-over-year. If you want to grow any faster, you need more drastic methods: I would suggest creating completely new teams on a completely new stack who just ignore everything that was there before, starting from scratch. Otherwise, all these new teams will largely spin their wheels. But since that is a rare case, let's explore the split approach a bit more.

{{< figure src="/blog/images/split.webp" attr="Photo by [Joshua Brown](https://unsplash.com/@joshbrown)" alt="Fork in the road">}}
  
This article is mostly about the human aspect of the team split and less about the HR process that accompanies it, as that part will likely be different in every company. 

## Teams are immutable

Before we start with really anything about the details, let's remind ourselves that ***teams are immutable***: It happens when you add or remove people from a team, but especially when you split a team, you end up with two completely fresh teams. That also means you will need to go through the team construction process and the 4 stages (of [Tuckman](https://en.wikipedia.org/wiki/Tuckman%27s_stages_of_group_development)) again, so you need to invest into teambuilding and it will take a while until everything is productive again. 

_Before it gets faster, it will first get slower._

That's why I would suggest only performing a team split when they are necessary, and as late as reasonable because there is a significant cost attached to it.

## Preparation

When a team split is the reasonable thing to do (which you probably can tell from your hiring plan or your 3-year roadmap), preparation is key: A team split can't be reversed and a badly executed split will inflict damage to the individuals involved and to the effectiveness of the teams created, so most of the work happens here.

### Name of the new Teams

Teams need names - they give identity and purpose. It's also a very first signal if your split makes sense at all. If you struggle to give your teams good names[^1], this would be a good point to reconsider or rework your split idea. A good name is not only descriptive but catchy - You want your peers in the company to learn the new terms fast, and people will only do that if it's easy, as they have their own changes to navigate or memorize.

After a team name was there I started "leaking" this information to the team members, explicitly without timelines, so that they can start to ingest the idea of an upcoming team split in the far future. It helps if that change doesn't come by surprise.

### Responsibilites of the new teams

In addition to the name, the responsibilities of the team need to be divided up. I am (like a lot of people) a big fan of [team topologies](https://teamtopologies.com/) and the models used in the book, and have used it successfully. Given where my tribe[^2] was located, I was usually trying to build stream-aligned teams and avoided platform teams. 

That sounds easy now, but I found a surprising push from the outside towards starting platform teams - but I find the danger of "overplatformication" real and didn't want to add a domain platform team, that lives on a product platform, that lives on a technical platform, which all resides in a cloud platform... you get where I am hinting at. Too many platforms get in the way of each other, and you lose the customer empathy you get from a end-to-end responsibility. 

***Build teams that will work well, not ones that will look good on the org chart.***

But cutting good stream-aligned teams is hard! The first few cuts were relatively easy, where we could still separate individual Bounded Contexts into individual teams (when using the language of "[Domain Driven Design](https://www.amazon.de/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)"). As we grew this stopped being possible, and we then tried to separate by the [Jobs-to-be-done](https://jobs-to-be-done.com/jobs-to-be-done-a-framework-for-customer-needs-c883cbf61c90) of the individual subproduct. 

For example, you can split most capabilities into a configuration team and a front-facing team. They both have end-to-end responsibility towards customers. There might be people who disagree with that approach and favor a split-by-function (e.g. Frontend and Backend teams), and they likely have a point. I still favor a team that can do everything it needs to reduce waiting times and dependencies, even if it brings some awkwardness.

### Mission and Vision

Once the responsibilities of today are clear, you should also prepare a long-term Mission and Vision statement for both teams. They need to make sense for both without mentioning the other team in there - that's a nice success marker. The mission of the team can be used as an "elevator pitch" to potential new team members. I love to use the team's mission statement for pitching the employer side during interviews.   

### Skillset required

With a good vision in place, you will know what kind of skills you need to have present in your team. If you match this against the skills you see in your original team as it stands, you get a pretty good idea of what you need to be hiring for.  And it's a fantastic opportunity to get a fresh batch of junior developers in (avoid the [senior trap]({{< ref "navigating_a_downturn#the-senior-trap" >}})))

### Grow until it hurts

There's probably no perfect moment to split a team: It's either too soon, or it's too late. Splitting is never easy for a team, as the team members probably have grown to like each other, they formed a stable performing unit and life was comfortable. A split is turmoil and uncertainty, so usually, no one is looking forward to it. I loved the idea from [Heidi Hefland in "Dynamic Reteaming":](https://www.heidihelfand.com/dynamic-reteaming/) You should probably lean towards splitting too late. When the people present in the teams can feel the overhead and tension from being too big, they will understand the need for a split themselves. When daily standups take too long and planning meetings are a drag, a team split will sound like sweet relief to everyone.

## Execution

Now let us bring the new teams into reality:

### End celebration

The large team-to-be-split needs closure: It's a fantastic opportunity to get together and reminisce about past wins and successes this team had. Glorious releases and glorious failures. Customer feedback and the worst outage you ever experienced. If you can meet in person, go get some nice food, fire up a photo show of previous precious moments, and celebrate.

### Split workshop

On the next day, it's game day: Have a workshop where the final team placements and timelines are decided. I liked the self-assign approach with guidance: I described what skills and levels I need in each team, and then worked with the group until everybody had a place. I think this prevents bad moods later on as people have agency about their fate. But on the downside it led to some anxiety on the team because the most important thing of "where will I be?" was open till the very end. You need to know your team member's needs and preferences to make a good decision here, I have seen both approaches going well if approached carefully. 

After that, you probably need to create a lot of artifacts: Wikis need to be split and updated, Boards newly created, slack/teams channels and email groups need to be configured. Bug tickets and tech debt plans need to be distributed between the teams. Get the group going to create these artifacts together, as their first founding task. I recommend buidling up a check-list over the weeks, as this is likely more artifacts than you are initially aware of :) Don't forget to let your HR know about the changes as well.

A well-made logo and memes help a lot to bring some fun to the workshop, it might be nice to schedule some time for that.

## Aftercare

After the split event, the teams will go back to a new reality the next day, but you should still be looking at a few things to make sure you will end up with two well-running teams:

### Make the names known

I think it's your, the leader's, job to be the "publicist" of the news: The rest of the organization might be reluctant to recognize the team split, and still refer to the old team. This will hinder the new identities from forming, so I suggest being insistent about that, changing wikis where you forgot, making sure people use the correct channels for support etc. Use whatever all-hands meetings you have to shout it from the rooftops, and communicate on all channels you have until the message has sunken in. 

### Invest in Team Building

The new teams will be going through new constitution phases. You are probably familiar with [Tuckman's 4 Stages](https://en.wikipedia.org/wiki/Tuckman%27s_stages_of_group_development) or other models that help you understand the processes. The important part is that just because you had a fantastic team before does not mean you will get two smaller, well-running teams for free. You need to put in the work again, twice, to achieve high-performing teams. 

### Understand expectations and realities

After some time has passed I used some 1-1 time with everyone to understand how close their expectations have landed compared to the new reality, and how they felt about the process of the split. It's a good time to learn for the next split to come.

[^1]: Prohibiting you give your teams silly names like the fictional characters. I strongly prefer team names that tell other people what the team is doing. It's clear what a "Time Tracking" team does, but I won't ever be able to remember what the Hufflepuffs and Slytherins do all day.

[^2]: Although the name comes from the dreaded Spotify model, that noone does anyway - here it just means "collection of teams that work on a product together"
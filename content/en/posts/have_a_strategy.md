---
title: "Have a strategy"
date: 2023-02-27T08:35:00+01:00
draft: false
featured_image: "/images/strategy.webp"
images: ["images/preview/strategy.jpg"]
tags: [People Management, Managing Managers]
---

A while ago I told one of my new Engineering Managers that I expect them to develop a strategy for their team. And oh my, were they confused by this ambiguous ask. I failed to explain this concept and my wish multiple times until we got it right, so this is both a lesson for me and for everyone else watching: 

As an Engineering Manager, how can you develop a strategy for your team? I believe understanding this is the difference between a mediocre Engineering Manager who keeps the lights on, versus a great Engineering Manager who makes a difference.

In terms of business speak, the word Strategy probably lost all meaning before I even joined the workforce. But as a working definition, we are talking about is ***a high-level plan that outlines how a long-term goal for the behaviour of the team can be reached.*** So that means, before we get all strateg-y up in here, we first need a goal. Please note that this is a much smaller thing than a complete [Engineering Strategy](https://lethain.com/engineering-strategy/), but just local to your team.

{{< figure src="/blog/images/strategy.webp" attr="Photo by [Aaron Burden](https://unsplash.com/@aaronburden)" alt="Sun and fog">}}

I find this topic a great example of the metaphor of "working ***on*** the organization" vs "working ***in*** the organization", thanks to [Benjamin](https://cto.coffee) for that beautiful metaphor.

## What's my Goal?

And you will find in most of the Engineering Manager Role descriptions something about ***high-performing teams***. When we talk over beers about our teams, they are all of course high-performing[^1], always. But in reality, this is where I see the real value added of Engineering Managers[^4]. So while it's almost painfully obvious, I like to start from here:

_If you can influence your team as a unit towards becoming a high-performing team, you made the most significant contribution you could do as a manager._

Of course, in times of crisis and chaos, you should choose a different north star for your team that you focus on instead. Is your team delivering software that causes outages every day? Then it's a good idea to work on that instead. 

Your strategic goal can and should change over time, but you should only have one at a time for your team.

## Identify the obstacles

Before we now can build our strategy, we need to identify what's standing between us today, and our dream state of a high-performing team. For this, you need to observe your team and be with them for a while.

I can think of a couple of starting points that you could do to understand where the team is at:

* Participate in all meetings[^2]
* Do pair programming and Ensemble/Mob Programming
* Fix bugs yourself
* Be on call and work on incidents
* Ask good 1:1 questions
* Get the external perspective on the team from peers and stakeholders

If you struggle to identify the obstacles, I would start by reading [Thinking in Systems](https://www.amazon.de/Thinking-Systems-Donella-H-Meadows/dp/1603580557), which helped me reason about teams as a whole, instead of just observing people on their own. But additionally, think about the teams that you were a part of in the past, especially the great ones. What was different there, compared to the one you see today? Or go around and look at other teams, maybe those with leaders you look up to, and see how they work.

## Strategy is "your way out"

So now you know what's holding your team back, and it's on you to figure out a way out of this. Since there are infinite problems, I can't lay all solutions out for you, but here are a couple of starting points to get you unstuck:

* Talk to your peers, your manager and your support network. Somebody might have seen something similar.
* Read [Accelerate](https://www.amazon.de/Accelerate-Software-Performing-Technology-Organizations/dp/1942788339)
* Read [Team Topologies](https://teamtopologies.com/book)
* Read [The five dysfunctions of a team](https://www.amazon.de/Five-Dysfunctions-Team-Leadership-Lencioni/dp/0787960756)
* Shoot me an email - I won't promise an answer, but if your question is interesting and I have some time, I am happy to give it a shot. 

When you think about mitigation strategies, try to avoid the grand gesture or the big change. Any meaningful change that sticks is gradual, and you will have to work on it for a long time until it's habitualized - Your team will regress quickly if you just throw a solution at them and then focus on something else.

It's important to know (and to balance) how newly derived strategy fits with where the total organization wants to go - I recommend having a look at my post about [Doctrine and Tactics]({{< ref "follow_the_doctrine" >}}). When I mean Strategy, I still talk about your local Strategy, which will be a tactical move inside a larger company Strategy. 

Sometimes you will just need simple solutions: The team is afraid to deploy? Find out why they don't trust the automation, test coverage and alerting. Improve the cause of the problem, then work on building the release habit.[^3] 

Other times, you need to understand the incentives that steer behavior. For example, you want more collaboration in the team, but the promotion process exclusively focuses on direct contributions - you won't be able to resolve this by just asking people to collaborate. They will go back to the old behavior that gets them rewarded as soon as you stop looking. 

## Sharing with the team
	
Should you share that insight and your plans with the team? 

Well, do you want to be the evil puppet player behind the scenes? I assume not - so sharing is surely appropriate. I found good subtle ways in sharing this, without being too blunt about it, via Retrospective: If you bring the observations and problems that you observe, there is a strong chance that your teammates agree. And often, they see the same remedies that you would have suggested. I think it's always better to have your team on board, if they actively support you with this work, you are a lot more likely to succeed and make new behavior stick.

## Example

_Ultimately, here's a hypothetical suggestion that I would expect from an Engineering Manager:_ 

---

I want to get this team to a high-performing state. 

I currently see three issues that are standing in the team's way: 

1. Our work packages are too big, making releases risky and painful.
2. We lack knowledge in `$technology` to work effectively on `$area`.
3. As a result, releases are risky and we tend to avoid them, making it worse and breaking our flow.

To improve that, I will 

1. Work with the team during planning, 
   to make better task breakdowns a habit. Most tasks should be of a size that's doable in less than a day.
2. Bring in some training for `$technology`. Everyone should be able to take any task that touches this area after training.
3. Ultimately, get the team to release daily.

---

Prepare something like that, and you will have a very happy Christian as your Manager :)

## But I don't wanna!

Fair question, why should you do this? With the neverending cycles and the daily spreadsheet madness coming from your friendly Technical Program Manager already driving you insane, why should you carve out the time you don't have to build a strategy? 

Of course, there is the noble goal of the greater good of the organization, but there is also a direct positive benefit for you: You will get recognized that you can turn things around. Most organizations are full of people who can handle the status quo, but very few can sustainably improve things. If you can make a meaningful difference with your strategy work, you might be rewarded with bigger and badder problems - which hopefully corresponds with career progression. 

It will also make you resilient. Imagine if you just go with the status quo, and the inevitable problems will occur, you have no tools to solve things. And as we receive the blame and pass the credit as Engineering Managers, you will find yourself in the pressure cooker with no way out.  

## And after that?

As it goes with bottlenecks - You fix one and you will immediately recognize the next one. This work never ends, but it's a lot of fun: Nothing brings me more joy than people growing in their team and having a ton of fun shipping amazing stuff. You got this!

Also, after you succeed - that stuff goes into your own brag document. It's easy to overlook, and since we pass the credit and take the blame, make sure that your wins get recorded and celebrated when it's perf time. It's also strong material for future behavioral interviews you might take as a candidate.

{{< signup >}}


[^1]: I stole that joke from the nice german-speaking Podcast [Engineering Kiosk](https://engineeringkiosk.dev/podcast/episode/44-der-weg-zum-hochperformanten-team/)

[^2]: It sounds totally obvious, but once you have a really well running team, you can phase out of some of the meetings to let others grow their leadership muscle. But I would always start with all meetings, and phase out gradually.

[^3]: Sometimes that was just me asking "So can we release this now that $X is done? Yes? Why don't we release it then?" over and over until they got so bored of me that they started releasing

[^4]: If you struggle to see the value that you add because you are not coding: Here it is. You are a multiplier now. 
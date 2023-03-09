---
title: "Architecture is everyone's business"
date: 2023-01-17T08:00:00+01:00
draft: false
featured_image: "/images/architecture.webp"
images: ["images/preview/architecture.jpg"]
toc: true
tags: [Technology]
---
Software Architects and their boxes and arrows: I have enjoyed working with some and suffered working against others in my career. I feel that in the majority of cases, the dedicated Role of "Software Architects" needs to be abandoned and the responsibilities need to be moved into the teams. This article outlines how this can be achieved by creating a rotating role called "Feature Owner" that enables the team to make the right local decisions and align themselves with the needs of the wider organization. 

What do I mean by that fuzzy term "Architecture"? Architecture is, as famously put, the part of Software Engineering that's hard to change later.[^1] As this isn't very helpful, for this Article I would suggest defining it as "Defining the Approaches, Plans and Rules how future software will be added to an existing Software Stack".

{{< signup >}}

{{< figure src="/blog/images/architecture.webp" attr="Photo by [Ryan Kwo](https://unsplash.com/it/@milkbox)" alt="Lighthouse in the Water ">}}

## The role of the Software Architect has lost its importance

Let's find out why I believe the Role of the Software Architect is no longer as useful as it might have been:

### Less standardization is needed: Contracts over specifications

The systems we build have changed since the days when the architect role was invented: As we got better at modularizing systems, the need for central architecture has diminished. It's not fully vanished, we'll get to this later. It becomes less important _how_ subsystems are implemented, as long as they comply with a defined set of functional and non-functional requirements: 
    
* With contacts about the behavior of the system in Place, like [API contracts](https://www.openapis.org/) and [CDCs](https://de.wikipedia.org/wiki/Consumer_Driven_Contracts), inner implementations can be different by component and chosen by the team

* As long as defined standards are upheld, like multi-tenancy protection or GDPR-compliant data deletion, inner workings can again be defined by the 

So from the generic idea of "Architecture", that we had in the days of J2EE Behemoths, we see a split into Macro architecture (how the larger system plays together) and local architecture[^2] (how a subsystem achieves its goals) 
    
### No plan survives contact with the enemy  

The enemy in our case is the pesky reality of building software that messes up our carefully thought-out boxes and arrow diagrams. I remember when I worked in [construction]({{< ref "gratitude" >}}  ), on any construction site we had a bunch of Plans in our hands, but they would usually have plenty of times small problems in them where you would have to improvise locally, for example, a pipe or wire would run in such a way that you couldn't install something else that was supposed to be there. 

To succeed, we improvised, and tried to get as close as possible while maintaining the original idea of the plan. In Software engineering, with many ways of automated verification and fitness functions and rigid rules, you have no such degree of freedom. Too many teams are forced to use weird workarounds to comply with a rigid architecture and cause stronger breakage because they still have to ship features: I have seen wide abuse of reflection because imports over module boundaries were banned. That wasn't detected but made everything a lot worse.


### Dedicated and isolated Architects create unhealthy team dynamics

In all organizations that I've seen in my career where designated architects existed (which is of course only anecdotal evidence), after a while the architects and the "regular developers" moved into an unhealthy power dynamic: The Architects assumed the developers to be bumbling cavemen (and -women) who couldn't write a for-loop without injuring themselves, and therefore need to be protected from their stupidity. The developers on the other hand thought of the Architects as power-trippy detached mouth-breathers who made insane rules for hypothetical systems that had no resemblance to the real demands of the business. Of course, there are other architects out there: Those that work hard to enable teams to accomplish their goals. These aren't so much the focus of this article

As the worst effect, the developers (who were indeed smart) had to spend a significant bunch of their time subverting the rules of the Architects in clever ways to get their features done. This angered the (also smart) Architects who in retaliation tried to tie the restrictions tighter to avoid further degradation of their pure and beautiful system. In that conflict, there were usually no winners, and the biggest loser was the customer.

### The architect title drives an unhealthy career dynamic

A concerning set of interview candidates and reports told me that they want to progress in their career toward a Software Architect Role because they want to be the ones making the rules. And when I pressed on why that is the case, it was usually a story of "Now I have to suffer these insane guardrails, but one day, I will be the one making the rules, and then the others will suffer" (Cartoonish laugh left to your imagination)

But what if - everyone could make the rules that they need because they have the larger guidance they need and the local insight that makes for good choices? 

A second dynamic we should avoid is that if architecture is explicitly one person's responsibility, other people don't care about it. The inverse of "If everyone is responsible, no one is" is true: "If one person is solely responsible, others will likely not care about it"

## Making Architecture everyone's business: The Feature Owner Role

Imagine after our successful mutiny, we ejected all our Architects into Orbit (or, more realistically, converted them to [staff engineers]({{< ref "grow_staff_engineers" >}}))[^3]. But as established, Architecture still needs to happen. It just has to happen at the right place by the right people. And to a large degree, that means it has to happen locally in the teams. To accomplish that, I had great success with the rotating role of the "Feature Owner".

The goal of the “Feature Owner” Role is to distribute that work in and broadly across the team, to allow for the growth and challenge of all Engineers. As a side-effect, this role can make the expectations clear and explicit, to transform them from an implicit to an explicit understanding of what needs to happen when a larger work item (which might be an Epic or a Story) is tackled by the engineers. 

The distribution of this role isn't a simple rotation, because the depth of challenge of each of the responsibilities is different per item, and we should examine closely what kind of work the Engineers of the team feel confident in taking on.

Every item that is "large enough" (could be "big enough to have an epic" and needing a discovery step by the PM). It’s the responsibility of the Engineering Manager to find a Feature Owner for each Feature.

### Lifecycle of the Role

The role should start way before the implementation of a work item: You want the corresponding engineer to be a peer to the Product Manager already during the early discovery phases. The role ends when the Feature is 100% released to all customers and all necessary cleanups are done (for example Feature Flags).

### Responsibilities

#### Architecture

The most important responsibility of the Feature Owner is to think carefully about the architecture of the feature. This prevents “accidental architecture” that might happen otherwise, or require dedicated architects. They're expected to consult experts from within and outside of the team as they see fit, as well as all guidelines available, examples being RFCs and our Tech Vision. The time required for this should be made explicit if needed. 

It is expected that the desired architecture will be documented in the form of an Architecture Decision Record or comparable format, as long as it's discoverable later. The Feature owner should evaluate different options of how a thing can be done, and weigh the pros and cons. The Feature Owner is expected to prepare a decision document and run a decision session with the team, and document the outcome of the meeting.

#### Refinement
To allow for effective team refinement meetings, the feature owner will collaborate with the product manager and/or the designer to break down the delivery work into user stories with acceptance criteria once the designs are finalized. It's expected that the breakdown of work is created and documented in JIRA. User stories should be max. 5 story points.

The team refinement meeting will be led by the Feature Owner, to share the overall idea of the Feature and task breakdown with the team. Changes during this meeting to the plan and architecture are welcome. 

It's not expected from the Feature Owner to come up with the perfect plan, but with the best plan that _they_ can come up with - as it is way easier to improve a plan collaboratively than to bootstrap one.

#### Communication
The Feature owner should be the primary point of contact for everyone else (including the PM and Designer), as soon as they assign themselves until the feature is released to 100% of customers.

#### Delivery
During Development, the Feature Owner is expected to watch for blockers or general Problems that might delay the Rollout, and collaborate with the EM or the Team to find solutions.

#### Rollout
The feature owner is expected to think about and propose a Rollout Plan and work together with the PM on it. The PM will be responsible for the overall Release Plan, which includes Documentation and written Communication with internal and external stakeholders.

#### Handover
Being Feature Owner shouldn't block anyone from going on vacation. If a longer absence happens during the active time of a Feature, the Feature Owner is supposed to name a substitute, and take the ownership back after their return.

#### Cleanup
If a Feature Flag was created during the rollout, and/or older logic and data needs decommissioning, it’s the Feature Owners' job to refine that work (for example to create Stories) and discuss them with the PM on where in the backlog they go. 

#### Non-Responsibilities
things the Feature Owner is _explicitly_ not responsible for:

##### Implementation
While the Engineer is of course welcome to implement parts of it, it's not the responsibility to implement all of it. Implementation is a team effort, and knowledge should be shared

##### Deciding Architecture
* The final Architecture is agreed upon in the Refinement by the whole team, where changes are welcome.
* Definition of “Features that need a Feature owner”

## Macro Architecture for larger problems that span multiple teams

As established before, only a set of problems can be solved locally and in isolation by the teams, and there are absolutely topics that the whole organization has to agree on. 

Are we back to having dedicated Architects? I don't think so (completely), there are ways in how the individuals from the teams can still influence the architecture of the whole organization: 

### Guilds and Communities of Practice

A "community of practice" or a Guild, if you like the terminology from the infamous Spotify model, is a group of representatives from the teams that meet frequently to align and decide on software architecture matters that are relevant to all of them. In such groups, topics of standardization can be discussed by the practitioners and common rules can be established. Since every team has a chance to influence the outcome, the buy-in is usually stronger. Also, the group with its diverse membership has a strong incentive to only work on topics that are relevant for a large number of members, avoiding going too deep into the individual team's lives.

Since I saw different implementations of this format with varying degrees of success, I think the differentiating factor of these groups is strong moderation. It needs a senior and communication-savvy person to prepare and run these meetings - otherwise, they become a coffee chat and don't produce tangible outputs.

### RFCs & ADRs

A complementary tool that works well is to have RFCs (Request for Comments): Larger strategy papers for intended architecture changes. These can be commented on, challenged and approved by a larger group of people and serve as a living record of the company's architectural journey, while keeping the reasons and discussions attached to it.

On the local side, a more lightweight format of an [Architecture Decision Record](https://adr.github.io/) can document internally what the team decided on and allow others to learn from other teams and understand their journey.

Much of this has been traditionally the work of Architects and can be democratized by using such approaches. 

All these documents should be public and presented in synchronous and asynchronous formats. If this becomes an organizational habit, "Architecture Drift" can be detected by peers and corrected as needed.

### The Architecture North Star

Software Architecture isn't a purely technical concern, architecture exists to solve business goals. Therefore, I think it's impossible to come up with a meaningful Software architecture without deeply understanding the business trajectory and future goals. 

Here's where I think one last "Architect" needs to stay: The technical executive. This would be a role equal to or comparable to the CTO: Somebody who is deeply involved in the business strategy (and knows things that aren't fully public to all employees yet). This person can and must describe the needs and demands of the software, and meaningful software architecture can be derived from this. The CTO can but doesn't have to, describe the larger outlines of the System's Architecture, but that can also be filled out by the communities of practice.  

## But how do we prevent the technology zoo?

A very interesting push-back I have received is, when there are no Architects, what's stopping the organization from creating a confusing technology zoo and introducing every shiny piece of alpha technology that they can find?

Although I agree with the goal of not having a zoo, I think it's very questionable to carry a whole role around just to prevent organizational dysfunction: Teams shouldn't do that by themselves, without some sort of supervision. There needs to be a culture of carefulness, but also the right incentives to use boring technology to solve exciting problems. I think that part belongs to the executive team to build the right incentives and guardrails - As usual, it should be easy to do the right thing, and hard to do the wrong thing.

This way, we can use these brilliant people that are currently inhabiting the Architect Role in a way more productive fashion.



[^1]: I think this term originates from [Evolutionary Architectures](https://evolutionaryarchitecture.com/), but I am not fully sure - ***Update*** [Victor](https://hachyderm.io/@kontrafiktion/109706081734787670) points out it's from [Ralph Johnson on the Extreme Program-
ming mailing list](https://martinfowler.com/ieeeSoftware/whoNeedsArchitect.pdf)
[^2]: I am not calling it micro architecture by intention as that term is usually used for CPU architectures, which is a way different level of "micro"
[^3]: There are people that try to define the idea of a "coding architect" to mitigate many points I am raising in this article, but polemically speaking I think that's mostly Architects that try to rescue their job for a little longer :-)

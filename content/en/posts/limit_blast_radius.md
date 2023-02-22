---
title: "Operational Excellence: Limit Blast Radius"
date: 2023-01-09T14:00:00+01:00
draft: false    
featured_image: "/images/blast.webp"
images: ["images/preview/blast.jpg"]
tags: [Operational Excellence]
toc: true
---

Trying to prevent all failures is a foolish endeavor. This doesn't mean you're not supposed to prevent and reduce failures as much as you can, but limiting the impact of failures turned out to be the most impactful strategy I found to improve Operational Excellence so far. In this article, we'll build a taxonomy of failure types and explore some strategies to limit the impact of these failure groups on your software system. 

The metaphor of "blast radius" describes how _far_ a problem in your system travels. In poorly resilient distributed systems, failures propagate and take usually the whole thing down with it.[^1] There are multiple dimensions of "radius" that you can tackle, and we'll take a look at them through this article:

> Everything fails, all the time. – Werner Vogels

{{< signup >}}

When I mean "limiting" the impact, I see 3 different dimensions in how we can contain problems within:
* a subset of your application - only one use-case will fail, others will keep working
* a subset of your users - for some of them a use-case will fail, for others, it will keep working
* a small amount of time - the use-case fails for everyone but comes back very fast

{{< figure src="/blog/images/blast.webp" attr="Photo by [Julius Drost](https://unsplash.com/@juliusdrost)" alt="Old chair in front of an abandoned and decaying wall ">}}

***Disclaimer:*** This article focuses a lot on large Web Applications - you might take some insights towards other types of Applications (like Mobile, or Embedded), but it won't be a full match. I also optimize my advice for enabling rapid development speed, instead of just testing everything in long cycles. That's because this article also rests on the shoulders of giants, namely the fantastic book [Accelerate](https://www.oreilly.com/library/view/accelerate/9781457191435/) which you definitely should buy and read. This book teaches us that optimizing for "Things never going wrong", will make them go wrong way harder, and impact your users stronger.

## Taxonomy of failures. 

Before we dive into mitigation strategies, it should help to have some taxonomy of failure types and group our mitigation strategies into these buckets. The buckets are chosen a bit arbitrarily: They are a simplified version based on [This paper from Microsoft](https://www.dropbox.com/s/23iv127vvi3az5d/incidents.pdf?dl=0) that I found via the excellent article from [Cindy Sridharan / Copyconstruct](https://systemsdistributed.substack.com/p/how-to-fight-production-incidents), and my personal experience in SAAS Products. Yours will likely be different. If you have some historical data already on where your system crashes the most, you have some idea of where to focus first. This serves as a good reminder to keep a solid record and history of your outages via [postmortems]({{< relref "oe_learn_from_failure.md" >}})

1. Code Change / Bug
2. Configuration Change
3. Dependency Failure
4. Infrastructure Failure

## 1 Code Changes

Any change to your codebase can potentially introduce outages. One example of Bugs that create outages are not logic bugs but incompatibilities in data structures, which generate exceptions instead of the expected result the client needs.

### Testing

I assume you have the very basics covered already: A sensible test suite, that is executed from within a CI/CD pipeline that deploys to production, and aborts on any failures. If you still ```rsync``` your ```index.php``` to your production env, maybe start with this. 

On a more serious note, from an incident perspective, I found the classical testing pyramid to be less helpful than having a stronger set of ***integration*** tests - Most Unit tests make sure parts of your logic works correctly - and your integration tests prove that the whole thing works at all. Outages usually come from things not interacting well together. If you find yourself in a situation where you have incidents created by complex intertangling of logic, you might shift "upwards" in the pyramid and do more integration tests than before, and reserve the Unit Tests for the places that do have actual logic in them.

### Separate Frontend and Backend

Most successful Systems start as Monoliths. That's perfectly fine, especially for earlier iteration speed. Very often you will use some server-side templating system from your initial web framework (like [Blade](https://laravel.com/docs/9.x/blade) or [Thymeleaf](https://www.thymeleaf.org/) or any of the others).

I found that from a pure resiliency perspective though, it helped a lot to ditch the original server-side templating for a solid internal API that gets consumed by a separate Frontend Application. Has anyone called that a ```duolith``` already? It doesn't matter much if it's a SPA Application or more classical websites with injected Javascript. It probably doesn't even matter if it's a separate Frontend at all, as long as you can untangle the frontend from the backend, and get some solid modularization in there. 

The problem with most templating engines is that there is no solid error boundary in the rendering stage - when some operation in the backend fails and an exception bubbles it, there is no automated way or easy way to inject a fallback state. With a dedicated frontend (and using some kind of fetch library)

I am fully aware of how insane that sounds - making a system significantly **more** complex and bringing network problems into the mix, to improve resiliency? Unfortunately, this was my historical best bet on introducing a solid error boundary at a point where it matters.

If you have multiple teams working on a shared space, [Microfrontends](https://micro-frontends.org/) look like another nice approach to contain errors within a certain domain.

### Use Feature Flags liberally

Feature Flags are an awesome tool for risk reduction, but you can also look at them as a blast-radius technique as well: If the change you're rolling out does indeed blow up, the impact is restricted to a subset of users. Additionally, it reduces your time to restore service if something goes wrong, because you can deactivate your feature flag usually with a click on some web interface, and your deployment will automatically serve the old implementation to everyone. I found it pays to have a great Developer Experience around feature flags (remember for every feature flag you add, you also need to remove it later on, so that better be cheap for developers to do)

### Canary Deployments

A canary deployment is one, where you roll out your change slowly and measure its success. If the error rate goes up compared to the baseline, the deployment gets aborted and you can re-work it before trying again. This reduces the impact to a random subset of users, and limits its impact also in time. The tuning of the parameters for canaries is a bit tricky, but I think quite worth it. This was my major advocacy in Personio in 2021 after running a manual analysis of 2020 outages. On a similar angle, Blue-Green deployments (and keeping a hot standby of your last, known good deployment) can help reducing the temporal aspect of the blast, because you can switch over almost instantly.

### Improve your rollback capabilities / MTTR

To reduce the "time under incident", you should take a look at your CI/CD pipeline to find out how to speed up reverting actions. For example, if you push a ```git revert #commithash``` your pipeline will likely execute a full build and test run - for a state of the repository that was already built, tested and released before your faulty release. If you can pre-run this pipeline with old, already verified builds, you will be back up faster. Of course, you should still git-revert and commit your change to avoid a re-introduction of the fault, and that might come with another "useless" build. But I would rather waste CPU cycles than my user's time. This is frequently talked about as Time to restore service, as described in [Accelerate](https://www.oreilly.com/library/view/accelerate/9781457191435/) 

### Harden your Dashboard / Homepage

Dashboards have an unlucky position - Usually, that's where everybody gets redirected after login, and where you will visualize a ton of data on it. That usually means a lot of core code is executed across all domains of your application when accessing this page. If anything goes wrong here - every user is effectively locked out of your system, as they land here after login, no matter where they want to go. That is a prime example of a very large blast radius, and smaller issues can propagate catastrophically. 

To harden your system, I would suggest doubling down on your error boundaries here - every "widget" on your dashboard should be evaluated if it can degrade gracefully if the underlying logic throws errors or is unavailable. If you don't have tooling available, you could try some DIY-chaos engineering audit and manually throw exceptions on all widgets to see what will happen.

## 2 Configuration Changes

I like to consider configuration changes a separate thing compared to code changes. Unfortunately, the configuration is usually quite powerful, and when it goes wrong, it's usually a pretty big disaster.[^2] 

{{< figure src="/blog/images/dns.webp" attr="https://www.cyberciti.biz/humour/a-haiku-about-dns/" alt="It's not DNS. There is no way it's DNS. It was DNS">}}

The absolute basis for all further tips is of course to run exclusively ```Infrastructure as Code``` where every aspect of configuration is in declarative text files, that get evaluated by your platform. Besides reproducibility, this also gives you some pre-checks if your configuration changes make any sense - but that's risk reduction, not blast radius reduction. If you don't have this and still make manual changes on the CLI on prod, start with this.
Many organizations have an environment called `staging`that is supposed to be a replica of your production system where you can test changes, even in an automated fashion. Unfortunately, that is never the case, and these systems are subtly different and give you a false sense of safety. Usually, they drift, and especially configuration changes have different effects whether the system has real traffic, or just sits there idle on smaller machines. Do yourself a favor and kill your staging env :-)

{{< tweet user="mipsytipsy" id="1308641574448803840" >}}

For pretty big config changes a "playground" environment can be useful though, to see if some big change works at all. But I would recommend spinning these playgrounds up and down as needed for individual, manual tests.

So what does this leave us? 

I believe that ***canary deployments*** are also a very useful tool for configuration changes when your configuration is applied as a step in your CI/CD pipeline. Unfortunately, this will probably prolong your rollout period, as config changes often don't blow up right away.

Besides that, the best lever I found is to improve Time to Detection and Time to Restore for such failures: Invest in great monitoring and observability tooling: Keep the noise down and when a faulty change gets pushed out, you will notice right away. Then you can quickly correct and limit the temporal impact of the problem.

## 3 Dependency Failures

> A distributed system is one in which the failure of a computer you didn't even know existed can render your own computer unusable -- Leslie Lamport

If your system grows and becomes more of a distributed problem, usually your rate of incidents grows: Unfortunately the uptimes of multiple systems multiply: 

Imagine you have two dependent Services A and B. If your service A has an availability of 99% and Service B has also an availability of 99%, the resulting availability is ```0,99*0,99=0,98```, so your complete system has only a 98% Availability. This is a very simple example indeed, but it drives home the point that if you have a distributed system with a high number of components in there, and if your architecture requires everything to be working all the time, you'll have a very bad time.

A lot has been written about proper resiliency patterns, and I can only scratch the surface here with some introductory teasers about patterns useful to limit the blast radius of outages. To prevent failures from cascading, you want to use patterns that try to ***isolate*** concerns. If you want to learn more, you can start with [this slideshow](https://www.slideshare.net/ufried/resilience-reloaded-more-resilience-patterns)

### Fallbacks

If you embrace failure when consuming anything from a dependent service, the easiest thing to do is find a fallback response if the service is not available. For (a simple) example, if you need a profile picture from an image service, you could fall back to a generic avatar that you have stored yourself. 

### Timeouts

Simple, but often forgotten to implement: If you call external resources over the wire, make sure to stop waiting at some point and return a graceful degradation if you don't get an answer in time. 

### Bulkheads

Borrowed from the idea of hulls for ships, you try to allocate only a limited part of the overall system resources to a certain part of your service - like a fixed thread pool. If one of your downstream dependencies acts up an a malicious way, it can't take your whole service down, therefore limiting the blast.

### Prefer asynchronous communication

Even though not fitting for every use case, when it's available to you it's quite helpful. If you can drop a message to another Unit in your system without waiting for approval, or reacting to an answer whenever it happens to be available, you are a lot less likely to be disturbed. There is a reason why Actor-based systems are amongst the most resilient applications.

### Retries, exponential backoffs and Circuit Breakers

Retries are again nice and simple but often forgotten: If your downstream dependency breaks, just try again. Sometimes, you'll get a reasonable answer next time around. To avoid avalanche-like problems though I would suggest to always combining retries with exponential backoffs, and if you really want to be nice to your downstream dependency, with circuit breakers. This way you'll improve your chance of rescuing your request (and not having a problem in the first place), without taking down the whole ship in the attempt to do so.


## 4 Infrastructure Failures

So your whole data center just went down, because _someone_ was not paying attention when digging a ditch with their excavator, cutting the powerlines to the DC? And the old diesel generators, after not receiving maintenance for a few years, didn't start to provide backout power? Or when ```us-east-1``` went down, you went down along the whole rest of the internet? 

This is one of the harder problems to avoid as other people are involved here, and usually, a costly one to prevent. If you can, running hot standbys in multiple Datacenters can help you here, but this has severe architectural implications. It's up to you to make a financial calculation if it's worth it to you. Speaking from a European perspective though - it makes sense to not run things in the one region that your cloud provider uses to beta test new features. I would always opt for more boring, but also more stable regions. 

But there will be smaller infrastructure failures - Bad machines, bad disks and bad network links will appear if you just run a large application long enough. I think your best bet is to treat them the same way as dependency failures from point 3 - by introducing resilience patterns into your stack. 

## How to know you are ready?

If you are already working against a stream of outages, you should hopefully see positive signals and fewer outages over time. But all of that could be a coincidence, so how do you know that the work outlined in this article has paid off? The answer is chaos engineering. The best way of knowing that your system is stable is by poking (controlled) holes into it, and watching how it behaves. The best-known actor on the block is surely the [Chaos Monkey](https://github.com/netflix/chaosmonkey) and the rest of the simian army from Netflix, who were pioneers in this area. By now there is a lot more tooling out there like [Steadybit](https://steadybit.com/) and many more. I think reading [Chaos Engineering](https://www.amazon.de/-/en/Casey-Rosenthal/dp/1492043869) might help as well.



[^1]: It's always helpful to remind yourself of the 8 fallacies of distributed computing: https://web.archive.org/web/20171107014323/http://blog.fogcreek.com/eight-fallacies-of-distributed-computing-tech-talk/
[^2]: In the fun series of "No way it's DNS... Okay it was DNS": https://blog.cloudflare.com/october-2021-facebook-outage/
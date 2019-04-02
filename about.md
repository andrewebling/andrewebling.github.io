---
layout: page
title: About
permalink: /about/
---

# Bio #

![Mugshot]({{ site.url }}./assets/photo.jpg)

I'm Andrew and I've been working on mobile software, of some description, for the entirety of my 18 year career-to-date.

Back in 2001, I helped implement a Java runtime environment for cross-platform mobile environment, before moving on to focus on J2ME, targeting phones with keypads and tiny screens (remember those?). Back then, I was one of a minority of users who downloaded `.jar` files and installed them to whatever Nokia phone I was using at the time.

Then the iPhone came along. As the iPhone was launched, I decided there-and-then to move to develop software for that platform. Of course, initially the platform was officially restricted to rather half-baked and rather unsatisfying web apps.

Unofficially, it was possible to jailbreak an iPhone, download an unofficial, reverse-engineered and undocumented SDK and hack together your own apps. During this time I cut my teeth in iPhone development by putting together a proof-of-concept port of the app which I was working on in the day job. The platform was very rough around the edges, but it was enough to convince me that the iPhone would be come a viable platform for apps.

As soon as the official iPhone OS 2.0 SDK came out, I set about scratching an itch - solving a real world problem I had; having ideas at inconvenient times. The result of this was [iBlueSky][1] - a mindmapping app, designed for capturing and developing ideas on-the-go. I learned Objective-C and iOS SDK development on-the-job - entirely self taught and with very little public information available. 3 months later, iBlueSky launched and was the second mindmapping app on iOS by a matter of days and went on to be featured on the front page of the UK App Store for 2 weeks.

A few years later, the iPad launched, providing an infinitely better platform for mobile mindmapping. 

![iBlueSky on iPad]({{ site.url }}./assets/ibluesky-ipad.png)

Once the initial "app goldrush" subsided, I worked on a variety of apps for different clients, while keeping iBlueSky going as a sideline. Eventually I went to work for [Shazam][2], inheriting a codebase with a rather checkered history, which was eventually re-written (test-first) in Objective-C, back when we were still `[myObj retain]` and `[myObj release]`-ing everything in the days before ARC. The end result was an app which was far, far more stable, started in a fraction of the time and [massively reduced the time taken to obtain a match][3] to a matter of seconds.

Fast forward several years and with the launch of Swift, I went to work on a greenfield Swift project. As with any new language or platform, initially, the tools and libraries weren't in place to support disciplined TDD, so this project was not developed test-first. Although the language was safer by design and far more bugs were caught at compile time, I really noticed the challenges associated with not working in a test-driven manner.

The next project, a music streaming app, was a combined Swift & Objective-C codebase, which had originally been written by an agency. It had hardly any tests and a high number of dependencies. The first few months were spent in damage limitation, ironing out a number of critical bugs, including an obscure but killer race condition around in-app purchases. Again, the absence of tests for supporting risk-free change was keenly felt.

Moving on a few more years and I went to work on a greenfield Swift re-write for a prestigious UK retailer. Working a part of a large team on an app with a VIPER architecture - here I really learned the benefit of well separated concerns and design for testability. I took this approach forward to my next project, which was consistently developed with code coverage in excess of 95%.

I'm currently taking a break to spend some time learning new skills and applying them to iBlueSky. Which is what this blog is all about.

 [1]:https://itunes.apple.com/us/app/ibluesky-mindmapping/id291664204?mt=8
 [2]:https://www.shazam.com
 [3]:https://mashable.com/2012/04/04/shazam-5-update/?europe=true#aLJqgZ_zvsqi
# Plotting a Course #

TL;DR - I'm taking a career break, to be documented here on this blog, aiming to "level-up" my development skills and tame legacy app codebases with TDD & Clean Architecture.

## Introduction ##

Having spent 18 years working almost entirely in mobile software, and approaching the mid-point of my career, it is time for a break. Time to learn new things, refresh, recharge and set a course for the future.

Over the course of my career to date, I have encountered and worked on a variety of different codebases. Some of these were relatively young, but developed under crunch pressure, others were older legacy codebases. Still others were brand new greenfield projects,  starting from a clean sheet, using the latest technologies and development best practices. Some projects involved fresh rewrites of existing apps, others involved adding new features to existing apps.

Just as codebases change and evolve over time, hopefully for the better, so developers themselves should be looking to continually improve and refine their skills.

Most developers, as they progress during their careers, go through a series of phases on any given platform or technology:

1. Just Shipping - starting from scratch and getting through to getting something shipped, with a minimal wider experience of the platform or technologies. Not writing tests.
1. Re-writing History - re-writing an existing app from scratch, aiming to avoid making the same mistakes again, hopefully employing better development methodologies - like defining acceptance criteria up-front and writing tests first.
1. Corralling Chaos - starting with an existing app with multiple challenges and a somewhat chequered history, putting out immediate fires, getting the whole thing under test, improving architecture through a series of small refactoring steps and positioning the codebase for future change.

Having made what I consider to be a solid progression through 1 & 2, would now like to bravely embark on 3. It's one thing to be able to write a new app 100% test-first and to create a clean architecture from scratch, but it is much more demanding to start with an existing, sprawling, untested codebase, with little or no sense of design or architecture, and corral it into something which can be understood, modified and extended easily and with confidence.

I have therefore decided to take the bold move of leaving my permanent role and take a 6 month break to make this transition.

The rest of this post outlines why and how I plan to do this.

## Motivations ##

### Background: The birth of an app ###

Back in 2007, I was a moderately experienced J2ME developer attempting to squeeze useful apps into candybar phones with keypads, minute screens (by today's standards) and ~100Kb of heap.  Hardly anyone knew apps even existed, and even those that did had to be pretty determined to find and install an app to solve a real world problem. And even then, the real world problem to be solved tended to be boredom - most people stuck to games.

Then the iPhone launched, and I made a decision there and then, to migrate to producing genuine life-improving software for this new platform. Of course, the platform initially was locked down via a [Sweet Solution][1], which in reality turned out to be more like Bitter Sweet than anything else, until Apple shipped the iPhone SDK 2.0 and the App Store finally launched. Undeterred, I used the unofficial/reverse engineered SDK and a jailbroken iPhone to get to grips with the emerging platform, prior to the launch of the official SDK.

At this time I had a recurring problem - ideas frequently came to me at the strangest and most inconvenient times and I wanted a way to capture these and develop them. As an avid [mindmapper][2], I wanted to be able to capture, develop and organise ideas on-the-go. And so, armed with a copy of the beta iPhone SDK, [iBlueSky][3] was born. Having dabbled with Objective-C on the Mac, and therefore undeterred by an apparent sea of square brackets, picking up the language was pretty straightforward and the platform APIs (e.g. UIKit & Foundation) were far cleaner and better thought out than most of the Java APIs I had used up until that point. Key concepts like delegates and target-action fell into place and became familiar territory pretty quickly.

Nevertheless, it took some time to find my feet on the platform and I found I had to write quite a lot of code to get things done - either because I was not aware of capability within in the early platform, or the platform lacked those capabilities. For example the first version of iBlueSky used SQLite for data storage, because Core Data did not exist. Nor were there nice 3rd party solutions or wrappers, or even convenient ways to integrate 3rd party code like Cocoapods or Carthage, which we use now.

A month or so into development, it became apparent that I had chosen quite an ambitious first app, but persisted and eventually shipped it soon after the App Store first launched. Download numbers were encouraging.

## Goals ##

My goals for this career break are three-fold:

### Learn, Recharge & Revitalise ###

Learning new things is my favourite way to recharge. I intend to learn about tools and techniques for working effectively legacy code - by this I mean essentially any code without tests. I will do this by reading books and blog posts, watching YouTube videos and reading documentation - see [Resources](#Resources) below.

### Apply - App Re-birth ###

As any platform or technology newbie, I made mistakes as I developed iBlueSky and the app codebase has made it through a transition for every single major release of the iOS SDK, from iPhone OS 2 to iOS 12. It also made the transition from being iPhone-only to being Universal, following the launch of the iPad.

During this time, it has shed some responsibilities to the platform (e.g. migrating from SQLite to Core Data). The codebase also pre-dates my becoming [test infected][4], having only minimal tests - mostly around the migration from SQLite to Core Data. 

And perhaps, most seriously, like many early iOS apps, it suffers from classic [massive view controller][6] syndrome.

Altogether, this means the codebase has a rather chequered history and is now what I personally would consider [legacy code][5]. The app has become hard to change and in so many ways, I now know better than I did then.

iBlueSky is therefore a perfect candidate to apply the theory and knowledge acquired during this break. My plan is therefore to:

1. Complete development of a work-in-progress new feature, using disciplined [Test Driven Development][7], writing new tests and code in Swift, wherever possible, and ship this release. I want to prove to myself it's possible to continue to develop an app with tests, even when you don't have the whole codebase under test.
1. Make minimal changes to get the remainder of the app under test.
1. Refactor the app into a [Clean Architecture][8], through a series of small test-driven changes, possible making use of [Reactive][9] [code][10], where appropriate, and where it simplifies and reduces code volume.
1. Extend the app to embrace a brand new vision (🤐 for now!), underpinned by a codebase capable of accepting bold new changes, made in confidence that nothing has broken.

### Deploy ###

With the App Store [having turned 10 years old][16], many apps are in a similar boat to iBlueSky - showing their age, developed by developers who were learning on the job, and who were on their own journeys to become better developers, on top of a rapidly evolving platform, and having become split across two development languages - Objective-C & Swift, or early in a stalled transition from to Swift.

Many successful app-centric businesses may take the opportunity to totally re-write their app; indeed many have done this, and I've been part of several re-write projects during my career. However I am now fully convinced that this is [usually a mistake][17], with some notable exceptions (probably the subject of a future blog post).

In recognition of this, and the fact I can now apply my experience to deliver more value in this area, rather than purely cutting code, I ultimately plan to deploy these new found skills and expertise by launching app turnaround consultancy services at the end of this career break.

## Resources ##

Key resources I've shortlisted to use during this career break:

### Books ###

[Working Effectively With Legacy Code - Michael Feathers][11]

[Clean Architecture - Robert Martin][12]

[Refactoring (2nd Edition) - Martin Fowler][13]

[Pragmatic Programmer - Andrew Hunt & David Thomas][14]

### Blogs ###

[Quality Coding][15]

[Use Your Loaf][18]

[Hacking With Swift][19]

[NSHipster][20]

[Swift by Sundell][21]

[Ole Begemann's Blog][22]

https://www.objc.io/

## Technologies ##

The following technologies will be on my shortlist for adoption, especially where it makes code cleaner, simpler and easier to test:

[RxSwift][9]

I will also be going deep on Swift <-> Objective-C interoperability.

## Skills ##

In terms of other skills I hope to invest in:

* Problem Solving - I'm a born problem solver, but I take a fairly intuitive and free-form approach. I'd like to build on that with a framework which will apply to both technical and non-technical problem solving.

* Google Ad Words - in order to launch a new consultancy business, I'm going to need to level up on cost-effective use of Google Ad Words.

* Focus - my previous role involved constant context switching and I need to re-learn how to obtain that laser focus I once had.

# Finally #

This will be a long journey, which will require stickability and persistence to complete. I will endeavour to blog regularly throughout the process.


[1]: https://www.macstories.net/stories/before-the-app-store-the-sweet-solution-of-web-apps-and-developers-relentless-passion/
[2]: https://en.wikipedia.org/wiki/Mind_map
[3]: https://itunes.apple.com/us/app/ibluesky-mindmapping/id291664204?mt=8
[4]: http://junit.sourceforge.net/doc/testinfected/testing.htm
[5]: https://en.wikipedia.org/wiki/Legacy_code
[6]: https://www.hackingwithswift.com/articles/159/how-to-refactor-massive-view-controllers
[7]: https://en.wikipedia.org/wiki/Test-driven_development
[8]: http://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
[9]: https://github.com/ReactiveX/RxSwift
[10]: https://github.com/ReactiveCocoa/ReactiveCocoa
[11]: https://www.amazon.co.uk/Working-Effectively-Legacy-Michael-Feathers/dp/0131177052
[12]: https://www.amazon.co.uk/Clean-Architecture-Craftsmans-Software-Structure/dp/0134494164
[13]: https://www.amazon.co.uk/Refactoring-Improving-Existing-Addison-Wesley-Technology/dp/0134757599
[14]: https://www.amazon.co.uk/Pragmatic-Programmer-Andrew-Hunt/dp/020161622X
[15]: https://qualitycoding.org/blog/
[16]: https://www.apple.com/newsroom/2018/07/app-store-turns-10/
[17]: https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/
[18]: https://useyourloaf.com/
[19]: https://www.hackingwithswift.com/articles
[20]: https://nshipster.com/
[21]: https://www.swiftbysundell.com/
[22]: https://oleb.net/
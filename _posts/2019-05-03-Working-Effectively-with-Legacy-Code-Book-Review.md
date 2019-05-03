# Working Effectively with Legacy Code - Book Review #

## Intro ##

_"Working Effectively With Legacy Code"_ by Michael Feathers is a classic title, and probably one found in many a developer's library, whether in physical dead-tree form, or electronic. As I'm sure was probably the case for many other developers, I originally bought this book when taking on the responsibility of maintaining a large, sprawling legacy code project. In that instance, I inherited the code for an app used by 100+ million users, written by a number of developers, all of whom had learned iOS development on the job, and none of which still worked in the business. The app suffered from fundamental memory management issues, giving rise to severe stability problems, and also consisted of a very large volume of code, considering the scope of implemented functionality.

Desperate for quick answers, and willing to try anything, I purchased, downloaded and started thumbing through the ebook edition and gathered that the approximate gist of the book was as follows:

1. Get the legacy code under test
1. Refactor it into something maintainable

...at which point I promptly put the book down, with an internal dialogue something along the lines of:

> _"Well, if this code was capable of being got under test, I wouldn't consider it legacy code"_

At this stage in my career, I was aware of Test Driven Development, even aware of some of the supposed benefits. But it was something which I aspired to, or applied pragmatically in certain limited scenarios, rather than actively sought to diligently and consistently practice. It wasn't until nearly 9 years later, having become _"Test Infected"_ and having worked on several Greenfield re-write projects, using disciplined TDD, that I really came to understand the true value of consistently writing code test-first, as well as the major benefits of maintaining a codebase with a comprehensive and complete set of tests.

The book and advice contained within it are designed to be programming language and target platform in-specific, with example code from C, C++ & Java.

## Structure ##

Broadly speaking the book is broken down into 3 key sections:

1. Mechanics of Change
 * covers the basics, the tools and the techniques for getting code under test, ready for refactoring
1. Changing Software
 * This is the meat of the book - effectively extended FAQ, covering common scenarios and conundrums, with a continued focus of getting code under test.
1. Dependency Breaking Techniques
 * Breaking dependencies is the key to getting code under test and ready for refactoring; this section expands on, and applies, many techniques from part 1


## Notable Content ##

The core of this book is very focused indeed on getting code under unit test, both as a tool for understanding precisely what the code does and to enable it's structure to be improved via refactoring, in lots of small steps. It doesn't cover integration or behaviour tests, which might leave users concerned that the nuts and bolts i.e. the minute details of the implementation, have been preserved, but the bigger picture has not. In reality, is is much harder to refactor the big picture and maintain higher level tests, which might explain this as an approach.

The Appendix gives one example of the most basic refactoring possible - extracting a method - but refers users to the canonical title on the subject by Martin Fowler for the details. I would say that "Refactoring: Improving the Design of Existing Code" by Martin Fowler really is required reading in order to make use of the tools and techniques used in this book.

Unfortunately the Kindle eBook version of this book did suffer from a number of issues. Firstly the code was not presented in a fixed-width font and often spanned several page boundaries, making it difficult to read and follow. I frequently found myself copying and pasting the code into a text editor, in order to be able to fully grok it. This shouldn't be needed. The eBook has been out for a long time and there don't appear to be any updates available, in contrast to many of the other technical eBooks I own.

There were also issues with navigation within the book - the top level table of contents links to another table of contents, which in turn linked to the contents of the book. This made finding the way around the book somewhat challenging and frustrating. In some places numbered bullet points appeared with large/incorrect numbers (possibly suggesting a signed/unsigned bug in the display code?!).

So knowing what I know now, I would probably buy the physical, dead-tree version of this book for future reference.

All that said, the content of the book really is excellent and I've already successfully used a number of the techniques to address the common "Massive View Controller" problem on iOS. In particular, the "Sprout Method" and "Sprout Class" lend themselves well to being used in Swift extensions of legacy Objective-C view controllers.

Besides presenting a wide variety of code modifying techniques, a number of visual techniques are presented, particularly as a means of understanding how a proposed change could affect code in an undesirable way, including the concepts of "Effect Sketches" and "Feature Sketches". As a visual thinker, who believes that a pen and paper (or iPad, Apple Pencil & Notability) are the most effective debugging tools known to mankind, this was particularly welcome and useful.

One of the aspects of the book that I appreciate the most was how it is able to change how you, as a developer, think about legacy code. Developers are perhaps prone to one of two extremes when it comes to working with legacy code - either tip-toeing around, deliberately minimising the extent of any changes (and in doing so, actually _adding_ to the problem), or advocating throwing the whole thing out and replacing it with a greenfield rewrite. Both of these approaches can end up being very costly to businesses relying on software and developers can rob themselves of valuable experience too. Working with legacy code and dealing with the long term implications of previous mistakes can be highly instructive and may prevent reoccurrences of the same problem in the future. It also robs developers of the opportunity of learning to think through a series of small changes (what all refactoring _should_ consist of), which gradually move a codebase forward and into a better overall state of health.

Given this book was originally published in 2004, it is fair to say it was ahead of it's time. Although TDD was introduced as part of the Extreme Programming manifesto in 1999, general adoption in 2004 would have been quite low. As such it has aged well and the examples use programming languages which are still in common use.

I believe this book will probably appeal most to, and be most useful to, developers with a strong existing and practical grasp of TDD. And putting the principles, techniques and concepts into practice will definitely make you a better developer. A good software developer knows and applies the rules and best practice of software development, but a great developer extends this by knowing when it is OK, or even beneficial, to bend or break the rules or lay aside received wisdom in the name of pragmatism. Indeed, this book is a nod in this direction - it openly acknowledges that getting code under test can sometimes involve a backward step or two (for example trading some encapsulation for testability), in order to eventually achieve a much superior end-result.
		
## Missing Bits ##

Although the book is quite comprehensive in covering techniques to get code under test, it doesn't go much further than that; it lays good foundations, but does not progress far beyond them. And there are definitely other elements to working effectively with legacy code - how to refactor in a series of very small steps to eventually achieve architectural level changes, or strategies for navigating and understanding large sprawling codebases, making full use of version control history to gain context, work estimation for planning purposes, discussion of version control branching models and other specific challenges associated with working in a team environment with legacy code. While there is some discussion around thinking through and understanding the likely impact of changes required to get code under test, these principles are not applied outside the specific context of getting code under test, which is at a very granular level.

Probably the most notable omission in my mind is the lack of discussion of Quality Assurance - for example finding out if there is a comprehensive regression test plan in place, before embarking on making code changes, and describing the process of working out what to test and then re-test when making (hopefully innocuous) changes. A full suite of unit tests is a great first line of defence against regressions, but as almost any developer will tell you, it is quite possible to have a high degree of unit test coverage (95+%), have all the tests pass, and still have the end user experience bugs and fresh regressions.

On balance, I think a more accurate and appropriate title for this book would have been: "Getting Legacy Code Under Test", or "Working Effectively With Legacy Code - Foundations"; it feels like there could be another whole volume to be had from the subject.

## Conclusion ##

When I first picked up this book, I think it's fair to say I was hoping for quick wins and easy answers; something to numb the pain and quickly get things under control. And as such, I was disappointed, to the extent of putting down the book after a chapter or two. But the unfortunate reality is, any experienced developer who has spent a significant amount of time working with legacy code, will probably tell you there are, sadly, no silver bullets.

Having returned to this book, with more experience under my belt, and a practical understanding of the benefits of disciplined TDD in a greenfield environment, I can say that ultimately the book does deliver on what it promises at a foundational level, by getting to the root of the problem - working with legacy code is hard, and without tests in place, you really are flying blind and are very likely to break things badly.

And so, it is definitely worth persevering through this book, even if the value of the approach is not immediately apparent or obvious. Many of the examples and related anecdotes make it clear that the author is bringing to bear several decades worth of experience - he definitely has the battle scars to prove it. I can confidently say it would take in excess of a decade of day-to-day experience of working with legacy code in order to absorb the level of knowledge and expertise demonstrated in this book. As such, it is a very good investment indeed.
		
## Further Reading ##

As alluded to in this review, this book doesn't provide a complete toolset for getting legacy code under control, but it does lay down the most fundamental foundation. In order to progress and put everything learned in this book to good use, it would be necessary to read these two titles as well:

* Refactoring - Improving the Design of Existing Code, by Martin Fowler
* Clean Architecture, by Robert C. Martin
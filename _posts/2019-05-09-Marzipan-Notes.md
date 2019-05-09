# Introduction #

Having been there in person to hear Apple announce UIKit coming to macOS at WWDC 2018, and with WWDC 2019 rapidly approaching, I thought now would be a good time to delve into "Marzipan" and see what all the fuss is about.

At this point in time Apple have only announced their intention to provide iOS app developers a way to jump-start porting their apps to macOS. There is nothing official shipping for developers to use at this time. They have also been dog-fooding the work-in-progress, to bring a couple of iOS apps to macOS, including News and Voice Memos. It seems likely that the first official developer preview is likely to be released at WWDC 2019. 

Despite the lack of an official release, the irrepressible [Steven Troughton Smith][3] has managed to reverse engineer the existing Marzipan implementation, shipping as part of macOS Mojave. And although his solution for obtaining a sneak preview is not suitable for actually shipping macOS apps, it does give developers like myself an opportunity to experiment, ascertain overall viability of an iOS to macOS port of an existing app, get early visibility of potential issues, as well as identify, define, and work on, any foundational work which might be required to support a production-ready macOS app in the future.

To road test the process of porting to macOS with Marzipan, I will be using my own mind mapping app - [iBlueSky] [1]. To give a little context, this app was written in Objective-C before the App Store first launched; I learned iOS development on the job writing this app (although I did have some background in Objective-C from tinkering on the Mac previously). iBlueSky was originally written agains the iPhone OS 2 SDK and has been through the transition to every new SDK as it has been released. When the iPad came along, it was upgraded to become a Universal binary. You might say the codebase has a somewhat checkered history! ;)


# Process #

The process I followed to get iBlueSky up and running with Marzipan went something like:

1. Clone https://github.com/steventroughtonsmith/marzipanify.git
1. Open `marzipanify.xcodeproj` in Xcode.
1. Select the correct Team under Signing and let _Automatic manage signing_ ~~break things really badly~~ do it's magic
1. Build the `marzipanify` console app, entering keychain password to allow codesigning to complete.
1. In the Project explorer, find `Products > marzipanify` and do `Show in Finder` to locate it (this will be needed when running it from the command line).
1. Switch to the iOS app Xcode project and change the deployment target of the project to be iOS 12.
1. Do a build and deal with any build-breaking fallout arising.
1. Double check codesigning settings are all good.
1. Remove all absolutely non-essential frameworks from the build process (e.g. Reveal, Dropbox etc.).
1. Comment out code which references problematic frameworks (MFMailCompose*, 3rd party frameworks not built against iOS 12 etc).
1. Do a nuclear clean build (important, or there will be code signing issues).
1. Rebuild the project for iOS Simulator (important - it needs to be an x86 build).
1. Locate the iOS app build product.
1. Run terminal command: `marzipanify <path to build .ipa>`
1. The icon for the app should have it's "no entry" overlay removed in the Finder.
1. Double click the app icon to open.
1. If the app crashes, check the contents of the crash log, rip out any more required stuff and rebuild. Rinse and repeat until the app runs.
1. Generate a set of headers from the private framework in `/System/iOSSupport/System/Library/PrivateFrameworks` (See Steven Troughton Smith's blog post for details).
1. Peruse the headers and add the ones that you want to use to your project.
1. Edit the headers, changing `#import` statements as required and comment out any lines which cause issues.
1. `#import` headers as required in the app source code.
1. Add code to the app to support a native macOS toolbar and hide any corresponding and now redundant iOS toolbars.
1. Profit!

Most of the effort involved in this was around troubleshooting build issues relating to bumping the project deployment target to iOS 12.0 - I was getting a persistent build error as follows:

```
CodeSign ~/iBlueSky-cynbtxotdgenizfgrcuqpurunkqe/Build/Products/Debug-iphonesimulator/iBlueSky.app (in target: iBlueSky)
    cd ~/ibluesky-ios
    export CODESIGN_ALLOCATE=/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/codesign_allocate
    
Signing Identity:     "-"

/usr/bin/codesign --force --sign - --timestamp=none ~/Library/Developer/Xcode/DerivedData/iBlueSky-cynbtxotdgenizfgrcuqpurunkqe/Build/Products/Debug-iphonesimulator/iBlueSky.app
~/Library/Developer/Xcode/DerivedData/iBlueSky-cynbtxotdgenizfgrcuqpurunkqe/Build/Products/Debug-iphonesimulator/iBlueSky.app: replacing existing signature
/.../Library/Developer/Xcode/DerivedData/iBlueSky-cynbtxotdgenizfgrcuqpurunkqe/Build/Products/Debug-iphonesimulator/iBlueSky.app: unsealed contents present in the bundle root
Command CodeSign failed with a nonzero exit code
```

...however, after some head scratching and online research, I eventually tried a clean build and this resolved the issue.

With that issue resolved, the result, prior to any code changes to specifically add support for Marzipan, looked as follows:

![iBlueSky on macOS]({{ site.url }}./iBlueSky-Marzipan.png)

Initial observations, as follows:

* The window resizes fine, probably as a result of adopting Autolayout. What a good decision that was, in hindsight.
* The app is able to run fullscreen on macOS out-of-the-box.
* The by default, app icon in the task switcher is a generic one - there are instructions in the referenced blog posts on how to fix this however.
* `UIMenuItem`s work OK, but appear in a vertical list, rather than a horizontal pop-up. Looks a bit alpha-ish, but I'm guessing it's probably non-final UX.
* `Cmd+Z` + `Shift+Cmd+Z` works fine for Undo/Redo respectively.
* Center-justified text in `UITextView`s ends up being right-justified.
* `UITextViews`s end up with a vertical scroll indicator visible, even when not required.
* There are a few challenges with scroll views:
 * Scroll bars are visible most of the time, but the behaviour around visibility is not very consistent.
 * It's not possible to pan around by dragging in the background; you have to drag the scroll bars (awkward) or use the mouse wheel for vertical scrolling and shift+mouse wheel for horizontal scrolling.
 * I wasn't able find any way to zoom using the mouse, and I tried all the modifier keys and the mouse wheel. This may mean it is necessary to add some addition macOS-specific UI to handle zooming.
* Currently no attempt is made to automatically translate iOS-style navigations and navigation bars into a macOS equivalent. Maybe this too will come in the first developer preview?
 
# Anticipated Challenges #

Based on this short experience of using iBlueSky within the Marzipan environment, I anticipate a number of challenges:

* As a so-called "shoebox" application (where all projects are held in one central database, held in the app sandbox), it will be necessary to somehow reconcile this approach with a typical file-based approach which is common on macOS. One option might be to introduce the concept of a document "Library", which is where all your documents live, but you can import/export files at will on macOS.

* Typically macOS productivity apps are capable of opening multiple documents in multiple windows, whereas iBlueSky, as a typical iOS app can only edit one mindmap at a time. This probably represents the most significant engineering challenge, as I'm fairly sure there are assumptions of only one mind map being edited at any one time in the code.

* In order to have a native macOS look-and-feel, it will be necessary to high existing iOS navigation and use a macOS style toolbar at the top of the app window. However, in Marzipan, this toolbar is at the `UIWindow` level, not at the `UIViewController` level. That means there will be lots of business logic to write and maintain to update the toolbar when transitioning between screens in the app. We currently get this for free on iOS, courtesy of `UINavigationController` managing the navigation stack and `UINavigationItem`s for us.
 
* Marzipan apps are currently scaled down to 70%. While mindmaps drawn via CoreGraphics look great on the iMac's built-in Retina display, the appearance is compromised when running on the external screen with a @1x resolution. Not only does this mean drawing and rendering challenges, but also means developers will need to go back to supporting @1x resolution displays in general, for everything else, especially graphical assets.

# Necessary Adaptations #

* Apps which make use of scroll views are probably going to have to find a better way to manage panning and zooming - these currently feel quite clunky. It is possible that the first developer release of Marzipan may fix this.

* Apps which do not currently offer any kind of cross-device syncing _must_ offer this if also running on macOS. iBlueSky currently falls under this category. Perhaps `CloudKit` is now up to the job?

* Apps are going to have to deal with more keyboard input and handle loosing and gaining focus within one editing session.

# Philosophical Differences #

* Good iOS apps really are distilled down to the absolute minimum - thought through, elegant simplicity and restraint are the order of the day. macOS apps, on the other hand, tend to be much more complex, fully-featured and flexible beasts.

* iOS apps tend to have straightforward, highly discoverable UI, which is presented only when it's required. Meanwhile macOS apps typically have more complex UIs, which required some exploration and elements which are not applicable tend to be disabled (e.g. greyed out menu items) when not required.

* Related to the previous point, iOS apps are optimised for touch control, which necessitates larger tap areas on buttons and larger spaces between buttons. macOS apps, being keyboard & mouse driven, typically have smaller controls, much more densely populated. Touch-friendly UIs from iOS might come across as overly simplistic and childish on macOS.

* iOS apps either rely on multitouch, or use gestures as shortcuts for something which could be achieved another way, but with less convenience.

* There has long been a significant gulf in pricing between iOS and macOS. The famous "race to the bottom" during the initial App Store gold rush push prices down to unsustainable levels. Meanwhile prices on macOS have remained more buoyant, where there is perhaps more perceived value. If single-purchase Universal apps will run across iOS & macOS, it will be difficult to strike an appropriate pricing compromise on both platforms.

# Conclusion #

Trying out Marzipan has been an interesting, if perhaps a little frustrating, experience. It takes me back to my early foray into iPhone development before the official iOS SDK was launched - indeed that too relied totally on `class-dump`ed Objective-C headers, along with a jailbroken device (rooted via a malformed image exploit IIRC) and an ssh session to copy compiled binaries across. The frustrations were similar too - a complete lack of both any documentation and almost any pertinent information online, including the ever-essential [Stackoverflow] [2].

All that said, I believe it has been a sound investment of time, as I now have a clearer picture of what will be involved in getting iBlueSky ready to make another platform transition to macOS. I therefore look forward to the first release of Marzipan. It's just a shame I won't be at WWDC this year to take my problems to the labs!

One final observation though - my gut feel is that if Steve Jobs was still with us, this project would not have made it out of the prototype lab; it may turn out to be expedient for developers, but I'm yet to see how well it will work out for the user. Time will tell.

# Links #

Steven Troughton Smith's groundbreaking work on unofficially opening up Marzipan, prior to official release:

https://www.highcaffeinecontent.com/blog/20190302-Making-Marzipan-Apps-Sing

https://www.highcaffeinecontent.com/blog/20190302-Making-Marzipan-Apps-Sing

https://www.highcaffeinecontent.com/blog/20190307-Deeper-Integration-with-Marzipan

https://github.com/steventroughtonsmith/marzipanify

Opinion piece from Craig Hockenberry:

https://blog.iconfactory.com/2019/05/what-to-expect-from-marzipan/

# Twitter Accounts #

https://twitter.com/stroughtonsmith

https://twitter.com/NSBiscuit

https://twitter.com/hbkirb

https://twitter.com/argentumko

[1]: https://itunes.apple.com/us/app/ibluesky-mindmapping/id291664204?mt=8 "iBlueSky"
[2]: https://www.stackoverflow.com "Stackoverflow"
[3]: https://twitter.com/stroughtonsmith "@stroughtonsmith"
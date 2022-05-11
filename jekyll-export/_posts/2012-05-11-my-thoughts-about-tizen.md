---
id: 2912
title: 'My thoughts about Tizen'
date: '2012-05-11T17:56:23+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2912'
permalink: /2912/
aktt_notify_twitter:
    - 'no'
categories:
    - 'Dev Talk'
tags:
    - tizen
---

After the Meego was dumped by Nokia, Intel and Samsung created an alliance to create new a Linux based mobile OS called Tizen. The Tizen is pretty close to the old WebOS with HTML5 application framework, and Linux kernel. The [Tizen SDK was published ](https://www.tizen.org/blogs/tsg/2012/tizen-1.0-larkspur)a while ago and it really doesn’t impress me at all.  
The whole Tizen SDK seems pretty useless to me. I don’t need this heavy SDK, and all of it’s simulator and emulators to develop HTML5 apps. Regular browser and JavaScript debugger is enough for me. The only reason for me to use the HTML5 to is the portability. The app should run on every platform Android, iPhone, wp7, Meego etc, so I really don’t see any reason to use Tizen specific API’s, instead I would use [Phonegap ](http://phonegap.com/)and build for multiple platforms instead of choosing only to build for Tizen.  
I guess that the HTML5 is good enough to build simple 2D-games by drawing into canvas, and writing the game logic with JavaScript, but It’s not that good for serious applications. The biggest problem with HTML5 apps with jQuery Mobile is the performance. Even on Samsung Galaxy SII you won’t get 60fps scrolling with basic list elements. You can test this by yourself by loading the jQuery [mobile demos](http://jquerymobile.com/demos/1.1.0/) page in your phone. After running the demos with few devices it seems that Apple engineers have optimized the webkit pretty well for the iPhone, but every other platform is just way too slow. Also the animations are pretty much useless on Android devices. Jittering happens all the time if you try to use the animations. I really hope that Intel and Samsung engineers are going to make huge optimization’s to the webkit, since otherwise the platform will be completely too slow, and unusable.  
I would like to have SDL and Qt frameworks as part of the Tizen to develop native apps. The Tizen is Linux based after all, so porting existing games and apps would be easy if SDL and Qt would be a part of the current platform. However I still have some hopes for Tizen, since it seems to me that any community member could port SDL or Qt to Tizen with the platform SDK, and add it into some repository for everyone’s benefit.
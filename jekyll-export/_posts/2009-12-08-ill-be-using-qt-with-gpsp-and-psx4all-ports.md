---
id: 1421
title: 'I&#8217;ll be using Qt with gpsp and psx4all ports'
date: '2009-12-08T16:58:26+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1421'
permalink: /1421/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Qt Development'
tags:
    - gpsp
    - psx4symbian
    - 'Qt Development'
---

Currently I have the dynamic recompilation running without the trampoline pattern (thanks to hinkka’s tips), so there’s no deoptimizations in the dynarec side anymore. However the speed is not nearly as good as it should be. It seems that the main issue is somewhere in the Symbian SDL port. Therefore I decided to dump the SDL port, and make my own port with Qt.  
The Qt will be the UI system for Symbian^4 and for future Maemo platforms, so they can easily be supported after this change. So basically I’ll be getting much better compatibility too. Actually the Qt is already working on the Current Maemo 5 and N900! The dynarecs were originally written for linux, so there really shouldn’t be any issues compiling and running the same SW with Maemo devices too.  
Using Qt with S60 versions from 3.1 to 5.0 is a bit more challenging. I doubt that the Qt’s blit is fast enough, so I’ll have to make old S60 blit-functions for them, but it’s OK, I’ll switch to the Qt blit later on.  
I’ll be using the [Qt 4.6 which was released a while ago.](http://qt.nokia.com/about/news/nokia-releases-qt-4.6)
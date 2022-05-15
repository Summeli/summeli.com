---
id: 16
title: 'Playing around with S60 5.0'
date: '2008-11-14T16:28:00+02:00'
author: Summeli
layout: post
guid: 'http://koti.kapsi.fi/~summeli/blog/?p=16'
permalink: /16/
aktt_notify_twitter:
    - 'yes'
categories:
    - 'Symbian Development'
tags:
    - S60
    - 'Touch UI'
---

![joystickexample_with_3dgameexample](/jekyll-export//wp-content/uploads/2008/10/joystickexample_with_3dgameexample-300x198.jpg)

I Downloaded the S60 5.0 beta SDK from forum.nokia. I wanted to do some prototyping with S60 5.0 and try out the the new touch screen features. The touch screen API itself is pretty much same as in Symbian OS (Eikon) environment. The HandlePointerEvent-function seems like same as in Eikon at least. I have developed for Eikon in the past, so it was quite easy to understand the new touch API.  

I ended up making a joystick simulation for the touch screen. The whole example is available at [ forum.nokia](http://wiki.forum.nokia.com/index.php/Simulating_joystick_with_touch_ui). If I would have a S60 5.0 touch screen phone, I could try how well my example would work with feedback engine. I suppose it could work quite well. The current example at forum.nokia isn’t complete yet, it’s missing support for 8-way controller and I rather would send “real” key events to the window server, so the integration would be easier, but the current example gives you the idea.  
I won a brand new N96 phone from my example at forum.nokia, so using some time for S60 5.0 study was really worth of my time. Simulating all controls for Snes isn’t possible with Nokia’s current touch UI, since it doesn’t support multi touch. I hope that Nokia will publish new multi touch phone, so I could get my snes9x port also running on new touch phones.  

I know that it’s funny to worry about the future phones, when I really haven’t even released anything yet. It’s just that currently I’m facing some problems with audio rendering and frame synchronization, which can be solved with new more powerful hardware. I’m not done with N95 yet. It’s really a powerful phone with good OpenGL ES acceleration, so it really should be possible.
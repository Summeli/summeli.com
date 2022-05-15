---
id: 13481
title: 'Welcome to my blog'
date: '2008-09-16T13:45:40+03:00'
author: Summeli
layout: post
guid: 'http://koti.kapsi.fi/~summeli/blog/?p=3'
permalink: /13481/
aktt_notify_twitter:
    - 'yes'
categories:
    - Planning
tags:
    - porting
---

Hi there, I finaly got my blog up and running. Currently I’m planning to release Snes9x port on N95. I have the source code from [ notaz ](http://http://notaz.gp2x.de) UIQ version and I’m using that as baseline.  
At first I thought that I only need to port everything into EKA2 model plus write my own launcher for the emulator. Currently it seems, that there is a lot more work to be done. The audio and video renderers must be rewritten for N95.  
I also encounttered some nasty problems during porting the assembly code into the N95. I thought that the ARM11 in N95 would run that code without problems, but I keep encouttering these “Signal Exception 0 received: A data abort exception has occurred ” errors after a while.  
Therefore I did what I had to: I backported the original C-core instead of the ASM-core. Currently I should be able to run the emulator and worry only about the rendering (sound and video) part.
---
id: 15
title: 'Utilizing multimedia keys on N95'
date: '2008-10-09T09:33:47+03:00'
author: Summeli
layout: post
guid: 'http://koti.kapsi.fi/~summeli/blog/?p=15'
permalink: /15/
aktt_notify_twitter:
    - 'yes'
categories:
    - 'Symbian Development'
tags:
    - N95
---

I just took an example from [ forum nokia example.](http://http://wiki.forum.nokia.com/index.php/TSS000432_-_Utilizing_media_keys) Currently it seems that, the example isn’t working. The volume keys are working just fine, but the program is unable to catch other media key events.  
Therefore I downloaded[ Magic keys.](http://www.symbian-freak.com/downloads/freeware/cat_s60_3rd/descriptions/systools/magic_keys_remap_and_extend_your_keyboard.htm) The problem with Magic keys is that it requires “ALL -TCB” capabilities, so the platform security must be hacked to use it. I’m not telling how to do it in here, but you will find the instruction with google, if interested. I remapped the multimedia keys to buttons 1, 2, 3 and 4. So now I can control the Snes as I originally planned. I will probably also port this to the S60 5.0 with the touch UI, so I’m not going to implement my own key handler for multimedia keys, unless I get an example that really works.  
I started to wonder how the magic keys are implemented, since it requires platform security hack. I’m quite sure, that the Magic keys application is a FEP (Front End Processor) for the window server. It will get all the key events from a window server first, and then it will forward the events into other applications. Implementing my own FEP also sounds like a nice idea, but I want to have my own app running without having to hack the phone.
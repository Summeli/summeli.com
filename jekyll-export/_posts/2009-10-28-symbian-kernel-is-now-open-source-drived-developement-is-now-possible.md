---
id: 1364
title: 'Symbian kernel is now open source: Driver developement is now possible!'
date: '2009-10-28T18:19:58+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1364'
permalink: /1364/
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - ARM
    - kernel
    - rvct
    - Symbian
---

The [Symbian has released the kernel as open source!](http://blog.symbian.org/2009/10/21/delivering-on-promises-come-out-to-play/) The development environment consists of:

- Open source kernel and other complementary packages
- RVCT 4.0 compiler: free for developers and companies of less than 20 employees
- Open source simulation environment based on QEMU
- Open source base support package for the low cost Beagle Board

The kit has everything required for Symbian kernel development. I’m planning on testing the new kit and investigating if it would be possible to make my own memory driver to flush the cache for executing code without creating a special memory chunk for the code and using the IMB\_Range deal.  
Why the this kind of driver is required, if the there’s already exist an API for self modifying code? Well, it would solve the memory mapping issue, which I explained on the post: [Why Symbian is so slow compared to Linux](http://www.summeli.com/?p=1143).  
The driver would give significant boost for all applications relying on dynamic recompilation, or self modifying code. This would give a big performance boost for emulators such as gpsp and psx4all. I think that the psx4all would probably be playable with the special memory driver.  
**Developing a driver:**  
The first phase would be to implement a test software, and the driver with the QEMU. If I’ll get this far, then I could think about purchasing the BeagleBoard, which could be used for verifying the driver functionality with the actual hardware. If the driver works on the HW, then it would probably work on the actual phone too. However, the Symbian platform security will be a big problem preventing the installation of the driver into an actual phone.  
  
**Symbian Signed:**  
The Symbian signed will be a big issue for the driver. I would have to get all capabilities from device manufacturers such as nokia, samsung, and sony ericson to get a legal certificate to install the driver. We all know that’s not going to happen.  
I think that the user should be able to turn off the f\*cking platform security if they want to. This could be even hidden under some special code, like the phone’s reset is currently implemented. Take also a look of the [red pill mode on maemo.](http://wiki.maemo.org/Red_Pill_mode) I think that Symbian needs something similar. Why not the user to bypass the platform security and let them have open devices.  
However, I know that there are already some hacks that can be used to install unsigned applications. You would have to do something like this to get the driver to work on an actual phone.  
**I don’t want to get your hopes up**:  
As already being said: The driver development is possible, but it’s not possible to utilize that driver on you own phone. I’m not going to make any hacks for your to help you with the driver installation. I’m only interested to get more speed to the emulators with dynarec. I’ll release all the source code as usual, but I’m not sure if there ever will be a change to create a valid sis installation file for the driver. It’s just a nice thing to try out with the QEMU and the beagleboard.
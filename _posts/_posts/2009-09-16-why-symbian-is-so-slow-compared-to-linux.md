---
id: 1143
title: 'Why Symbian is so slow compared to Linux'
date: '2009-09-16T17:25:35+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1143'
permalink: /1143/
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - linux
    - Symbian
---

Symbian phones are really slow compared to Linux based devices like gp2x etc. You really don’t get even near to the same performance (in frames per second) with Symbian phone compared to an open Linux device with similar ARM processor.  
Here’s couple of reason’s affecting my emulator ports.  

### 1. No direct access to the frame buffer  

Symbian doesn’t provide direct access to the frame buffer. The CDirectScreenAccess API is far from direct. All data goes through window server, so there’s cycles consumed in the sceduling (few context changes etc) and in the memcopy operations made by the Window Server. I’m assuming that the Window Server makes a transformation of the data passed to it via CDirectScreenAccess. This all makes the basic blit operation really slow in Symbian.  
I’m hoping that the Qt will provide faster access to the the frame buffer, which could provide significant speed increase to my emulators.  
### 2. Memory mapping and dynarec   

The memory mapping affects only gpsp-emulator, but it affects to it heavily. I have to use the [memory trampoline pattern](/1106) to get the dynamic recompilation working in Symbian. This affects all the dynarec emulators a lot. I’m quite sure that psx4symbian would be possible with OMAP3 based devices, if Symbian memory mapping could be modified.  
I don’t think that Symbian is going to change their memory mapping just to get dynarec emulator to run faster. However I’m quite sure that this also slows down all self-modifiyingcode which is being run in the Symbian OS, so there might be a little hope. At least I could add an idea about modifying the memory mapping into the Symbian Foundation’s idea database.
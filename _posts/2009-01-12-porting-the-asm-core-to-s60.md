---
id: 153
title: 'Porting the Snes9x ASM core to S60'
date: '2009-01-12T10:04:07+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=153'
permalink: /153/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - AntSnes
    - ARM
    - assembler
    - porting
---

As you all saw the emulator is really slow and the sound is not supported because of too much frame skipping. I have been working with ASM core (written by notaz) some time now, and it’s very frustrating. Currently I have the ASM- core running on N96 with ARM9 processor, but it’s crashing with N95 with ARM11 processor.  
The speed increase is really nice for N96, but it’s still not enough. The S60 DirectScreenAccess plus one extra memcopy for each frame buffer is draining all the power from the phone. With N95 and OpenGL ES it might be possible to emulate sound, if I manage to get it up and running.. The DSA issue is also very frustrating, since we were able to write directly into the devices frame buffer before 3rd edition and platform security.  
Currently the ASM port also has some other strange issues. The colours get distorted in some views. You can see an example on below. It’s really strange since, the same renderer works with the normal c-core.

![mario kart startscreen with ASM core](/wp-content/uploads/2009/01/asmcore_mariocart1.jpg)

mario kart startscreen with ASM core

![Mario kart distorted screen with ASM core](/wp-content/uploads/2009/01/asmcore_mariocart2.jpg)

Mario kart distorted screen with ASM core

This seems like a good opportunity to learn something from S60 phones and ARM assembler. - Why the ASM-core crashes on N95, The core is ARMv5 binary and ARM11 should be to run ARMv5. The N96 and ARM9 processor seems to be able to handle it.
- The strange frame distortion. I suspected a compiling issue for a long time, and it still could be the reason. However I spend hours of comparing the code to [DrPocketSness](http://reesy.gp32x.de/DrPocketSnes.html). And there really aren’t any big changes, so it’s really frustrating.
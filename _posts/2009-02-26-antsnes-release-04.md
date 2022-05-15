---
id: 332
title: 'AntSnes release 0.4'
date: '2009-02-26T17:46:23+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=332'
permalink: /332/
aktt_notify_twitter:
    - 'no'
syntaxhighlighter_encoded:
    - '1'
categories:
    - 'S60 3rd edition'
tags:
    - AntSnes
    - S60
---

Whats new

- it’s faster – a bit 🙂
- Keys in Landscape mode are fixed
- Removed the P.I.P.S dependency. P.I.P.S installation isn’t required anymore, so it’s easier to install 🙂
- Right softkey exit removed, so the application doesn’t exit by accident anymore
- support for 352 x 416 resolution
- Opengl ES support is back. I heard that this is nice feature for TV.

TODO’s for 0.5 release:

- Audio support. After many test cases I’m confident, that the phone performance is enough for sound emulation. There must be a bug in my port 🙁 I hope to find it for the next release.

### Installation:
P.I.P.S dependency is gone, just download and install  
### Video settings:  
Video Renderers

- DirectScreenAccess -Default, works in every phone
- OpenGL ES 1.1 – Works in OpenGL ES 1.1 enabled devices
- AntiTearing DSA – Experimental, it should remove tearing effect, works only in few phones. Do not even try with Samsung phones. The antitearing DSA might help for roms that run too fast (ie. the screen is updating more than LCD’s refresh rate, and there is tearing API). I’m just starting to test this ( new phones coming to markets etc 🙂

Screen Orientatuions:

- portrait – Default
- Landscape – Normal landscape
- N-Gage – landscape, but image is upside down. It’s meant for phones with “n-gage mode” like N95 and N96. The N96 can use the multimediakeys by default, but N95 users must use [Magic keys](http://www.symbian-freak.com/downloads/freeware/cat_s60_3rd/descriptions/systools/magic_keys_remap_and_extend_your_keyboard.htm) to map keys 1-4 to multimediakeys.

The Video settings modification takes effect, when AntSnes is started next time( a restart required).

[N96 keymap](/wp-content/uploads/2009/01/n96_keys-300x198.jpg)

### Key config 
Start key config to configure keys. The multimediakeys are not supported in the key config, but you can use any normal keys in here.  
Download:  
Sis file: [antsnes\_v04.sis](/wp-content/uploads/2009/02/antsnes_v04.sis)  
sources: [antsnes\_v04.zip](/wp-content/uploads/2009/02/antsnes_v04.zip)
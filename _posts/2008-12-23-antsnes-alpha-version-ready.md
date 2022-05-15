---
id: 28
title: 'AntSnes alpha version ready'
date: '2008-12-23T09:11:19+02:00'
author: Summeli
layout: post
guid: 'http://koti.kapsi.fi/~summeli/blog/?p=28'
permalink: /28/
aktt_notify_twitter:
    - 'no'
syntaxhighlighter_encoded:
    - '1'
categories:
    - 'S60 3rd edition'
tags:
    - AntSnes
    - N95
    - N96
    - S60
---

My Snes9x port to S60 is somewhat working and the alpha-version is ready for download. I have been testing AntSnes with N95 and N96, but I assume that it will run on other 3.1 and 3.2 S60 phones as well. Please send a comment if you are using it with some other phone. Please also keep in mind that this is the first alpha version, and I haven’t tested it much, so any problem reports are welcome to the comments.

With N95 the frame rate is decent, but you must install the [Magic keys](http://www.symbian-freak.com/downloads/freeware/cat_s60_3rd/descriptions/systools/magic_keys_remap_and_extend_your_keyboard.htm), to get the multimedia keys working. Unfortunately you must hack your phone for magic keys installation. There is nothing I can do about it. Use the Magic keys to map keys 1-4 to play, stop, forward and backward buttons. Start/select are mapped to volume up/down keys on the side.</span>

The N96 multimedia keys can be used directly, so there is no need for magic keys. Unfortunately the N96 is much slower than N95. The n96 has only ARM9 processor running 260 MHz and no OpenGL ES hardware acceleration, and N95 has ARM11 running 330 with OpenGL ES hardware acceleration. Therefore I made two different packages, one for directscreenacces and one for opengles (I will combine these in the future, when I have a settings dialog). The AntSnes\_dsa\_alpha is faster for N96, but the there is no interpolation, so the size of a frame is 256×224(NTCS) or 256×248(PAL). The AntSnes\_gles\_alpha can be used with N95. I haven’t run benchmarks which are faster in N95 the gles, or dsa package. They both should work though.

The current source is based on Zodd’s snes4iphone and Notaz snes9x for UIQ. Thanks go for Zodd, notaz and for all the original snes9x developers. I will also publish my sources soon.  

TODOs:

* Sound support
* Interpolation to full screen
* Settings menu
* Known issues:
* The dsa version seems to be freezing at time to time with my N96

### Installation:

I expect this to work on S60 3.1(Feature pack 1) and 3.2 phones. If you don’t know if your phone is S60 3.1 or 3.2, see [http://wiki.forum.nokia.com/index.php/S60\_phones](http://wiki.forum.nokia.com/index.php/S60_phones)  


Just install the sis package to the phone. Download links below.  


[antsnes\_gles](/wp-content/uploads/2008/12/antsnes_gles.sis) and [antsnes\_dsa](/wp-content/uploads/2008/12/antsnes_dsa.sis)  
Merry Christmas  

-Summeli
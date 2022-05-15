---
id: 1980
title: 'gnuboy v0.5 for Nokia S60 5th edition'
date: '2010-10-13T18:57:43+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1980'
permalink: /1980/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'S60 5th edition'
tags:
    - gnuboy
---

The gnuboy is a gameboy / gameboy color emulator, and now it’s ported for S60 5th edition. This was mainly made for the people who asked for gb / gbc support for gpsp. It was much easier to make by compiling a new emulator for S60 😉  
There’s no support for SE / Samsung. However it could be added by implementing the DSA changes described[ in my blog post](http://www.summeli.com/?p=1875).  
I have to admit that this is still quite unfinished. I pretty much ran out of time. The N8 is coming and I want to start optimizing all my emulators for Symbian^3. Finally getting to use the new graphics architecture, real MultiTouch etc. I’m sure you all know what I mean 😉

![](/wp-content/uploads/2010/10/gnuboy_menu.jpg)

  
### know issues:   
- No audio
- The’re a bug with .gbc extension. Rename your .gbc file into .gb, and you’ll ab able to play gbc games also
- SE and Samsung phones are not supported, sorry
- The D-PAD is not fully working. You need to press some other spots before you’re able to press the same button again. I’ll fix this in the next update.
- it’s quite unfinished, waiting for my N8 😉

  
### Installation:    
Same process as with other emus:  
1\. First Install Qt 4.6.3 binaries into your phone

- Nokia users can just download and install this [Download Qt installation package](ftp://ftp.qt.nokia.com/pub/qt/symbian/4.6.3/qt_installer.sis)
- No samsung / SE support in this one

[ ](ftp://ftp.qt.nokia.com/pub/qt/symbian/4.6.3/qt_installer.sis) 2. Download the gnuboy.sis  
3\. gnuboyrequires the **SWEvent** capability. The SwEvent is required for key mapping: Now you can map call/end call etc. buttons for the gnuboy usage. Therefore the following step is required to install the SW.  
Go to SymbianSigned and sign the gnuboy.sis for your own phone IMEI  
using free Open Signed Online option <https://www.symbiansigned.com/app/page/public/openSignedOnline.do> this operation should be free of any charge.  
Read carefully the instructions on the SymbianSigned site.  
You must give them

- Your Phone IMEI (you can obtain it digiting \*#06# on your phone)
- Your EMAIL Address
- gnuboy SIS Package

And then the symbiansigned should email you the signed gnuboy your phone. This package will be installable ONLY on your phone. This procedure works for all Symbian S60V5 Phones. I had also to change to date on the phone into yesterday to get it working..  
The alternative method is to hack your phone! You can find pretty good instructions from [MameXM download site.](https://sites.google.com/site/mamexm/Home/download-1-03) (scroll to the bottom of page: Signing &amp; Installing).  

### Download:     
Download the gnuboy: [ gnuboy (23302 downloads) ](/wp-content/uploads/downloads/2010/10/gnuboy_v05.sis)  
Sources are available on Github:[ https://github.com/Summeli/gnuboy4Symbian](https://github.com/Summeli/gnuboy4Symbian)
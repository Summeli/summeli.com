---
id: 2386
title: 'AntSnesQt 0.7: Audio update for S60 5th edition'
date: '2011-05-12T23:51:47+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2386'
permalink: /2386/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'S60 5th edition'
---

AtnSnes is Snes9x emulator for Symbian. It is actually based on [DrPocketSNES](http://reesy.gp32x.de/DrPocketSnes.html "DrPocketSNES") version 6.4.4, which in turn is based on snes9x 1.39. This one will only work for S60 5th edition phones. Symbian^3 users, don’t bother trying, the [AntSnes 0.8.1 for Symbian^3](http://www.summeli.com/?p=2384) should be much better for you.  
The new AntSnesQt comes with the audio fixes from clpalmer.  
**What’s new**

- Audio is now working
- fixed the crash after loading a second ROM

<div class="wp-caption alignnone" id="attachment_1697" style="width: 310px">![](/wp-content/uploads/2010/05/largeDPad-300x169.jpg)The Big D-Pad

</div>**Know issues:**

- PAL ROMs do not work

  
**Installation:**  
1\. Qt 4.7.3 is required. The easies way to get the Qt installed is to install Flowd from ovistore: <http://store.ovi.com/content/118220>  
2\. Download the AntSnesQt.sis  
3\. AntSnesQt requires the **SWEvent** capability. The SwEvent is required for key mapping: Now you can map call/end call etc. buttons for the AntSnes usage. Therefore a new step is required to install the SW.  
Go to SymbianSigned and sign the AntSnesQt sis for your own phone IMEI  
using free Open Signed Online option <https://www.symbiansigned.com/app/page/public/openSignedOnline.do> this operation should be free of any charge.  
Read carefully the instructions on the SymbianSigned site.  
You must give them

- Your Phone IMEI (you can obtain it digiting \*#06# on your phone)
- Your EMAIL Address
- AntSnesQt SIS Package

And then the symbiansigned should email you the signed AntSnesQt for your phone. This package will be installable ONLY on your phone. This procedure works for all Symbian S60V5 Phones.  
The alternative method is to hack your phone! You can find pretty good instructions from [MameXM download site.](https://sites.google.com/site/mamexm/Home/download-1-03) (scroll to the bottom of page: Signing &amp; Installing).  
4\. You might get warning like “not compatible with phone” just keep on going, it might still work 😉  
\[ad\]  
**Download:**  
Download the AntSnesQt: [ AntSnesQt v071 (19926 downloads) ](http://summeli.com/download/11276/ "Version 0.71")  
Sources are available on Github: <http://github.com/Summeli/AntSnes> (remember to choose the S60 5th edition branch)  
**Read this before posting comments:**

- Do NOT Ask where to find ROMs / Bios. Asking about these will just get you banned!
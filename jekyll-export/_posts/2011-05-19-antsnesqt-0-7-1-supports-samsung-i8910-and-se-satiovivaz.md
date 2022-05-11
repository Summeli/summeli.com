---
id: 2495
title: 'AntSnesQt 0.7.1: Supports Samsung I8910 and SE Satio/Vivaz'
date: '2011-05-19T18:44:30+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2495'
permalink: /2495/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'S60 5th edition'
tags:
    - AntSnes
    - i8910
---

AtnSnes is Snes9x emulator for Symbian. It is actually based on [DrPocketSNES](http://reesy.gp32x.de/DrPocketSnes.html "DrPocketSNES") version 6.4.4, which in turn is based on snes9x 1.39. This one will only work for S60 5th edition phones. Symbian^3 users, don’t bother trying, the [AntSnes 0.8.5 for Symbian^3](http://www.summeli.com/?p=2453) should be much better for you.  
The newest update adds support for Samsung I8910 and Sony Ericsson Sation and Vivaz.  
Thanks for the Samsung &amp; SE support for faenil <http://i8910tuning.com>  
**What’s new**

- Works now on Samsung I8910 and SE Satio/Vivaz
- Fixed manual frameskip ( you’ll still get crashes if you change it away from AUTO with Audio ON, so using that option is not recommended)
- Fixed a crash: “if no ROM was selected and you pressed a continue the emu crashed.”

<div class="wp-caption alignnone" id="attachment_1697" style="width: 310px">![](/wp-content/uploads/2010/05/largeDPad-300x169.jpg)The Big D-Pad

</div>![](http://www.summeli.com/wp-includes/js/tinymce/plugins/wordpress/img/trans.gif "More...")  
**Know issues:**

- PAL ROMs do not work’
- The volume control slider works only if you drag it into new position (tapping a new level doesn’t work)

  
**Installation:**  
1\. Qt 4.7.3 is required.

- **Nokia Users**: Download Install [ QT 4.7.3 for S60 5th edition (5049 downloads) ](http://summeli.com/download/11298/) and [ Qt Mobility 1.1.3 for S60 5th edition (3412 downloads) ](http://summeli.com/download/11300/)
- **Samsung &amp; **Sony-Ericsson** Users:** faenil has made a package for you guys. You can download it at: [http://www.olcso-tarhely.com/faenil/Qt\_4.7.3\_libs.zip](http://www.olcso-tarhely.com/faenil/Qt_4.7.3_libs.zip) (QtMobility is not required for AntSnes)

2\. Download the AntSnesQt.sis  
3\. AntSnesQt requires the **SWEvent** capability. The SwEvent is required for key mapping: Now you can map call/end call etc. buttons for the AntSnes usage. Therefore a new step is required to install the SW.  
Go to SymbianSigned and sign the AntSnesQt sis for your own phone IMEI.  
Step 1. Register to symbian signed [https://www.symbiansigned.com/ ](https://www.symbiansigned.com/) Gmail / Hotmail email adresses are banned from the symbian signed site, so you must use some other email service provider.  
Step 2. Sign the sis-file by yourself with the symbian signed web UI.

- Your Phone IMEI (you can obtain it digiting \*#06# on your phone)
- Your EMAIL Address (gmail hotmail etc. are banned, however Nokia’s email address is working)
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
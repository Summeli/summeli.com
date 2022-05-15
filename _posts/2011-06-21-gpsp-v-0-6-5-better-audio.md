---
id: 2557
title: 'gpsp v. 0.6.5 Better Audio'
date: '2011-06-21T22:45:45+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2557'
permalink: /2557/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'S60 5th edition'
tags:
    - gpsp
---

the gpSP is a gameboy advance emulator originally written by Exophase. And now it’s ported to the Symbian OS! This version is only for S60 5th edition. Symbian^3 users should use [gpsp 0.7 for Symbian^3 ](/2520)  

### What’s new:   

- Better Audio!
- save/load states is now working

![](/wp-content/uploads/2010/07/gpsp_051.jpg)
   
### know issues:   
- not working on Symbian^3 based devices such as N8
- It’s a gpsp port, so see the gpsp compatibility list before complaining about non-working ROMs
- the emulator crashes if you try to load a ROM without setting the BIOS
- there are some limitations in the ZIP file support, so maybe you have to upzipt the ROMs
- The ZIP files seem to be eating quite a lot of RAM, so If ROM doesn’t work, try extracting it.
- Samsung blit fails when “keep aspect ratio” is ticked off
- N97 CFW: You can not use touch + call buttons at the same time with this firmware.

### ZIP limitations    

- WinZip
- Roms ziped in the WinZip Maximum (PPMd) format WILL NOT work.
- Roms ziped in the WinZip Maximum (bzip2) format WILL NOT work
- Roms ziped in the WinZip Maximum (Enhanced Deflate) format WILL NOT run
- Roms ziped in the WinZip Normal format WILL run
- Roms ziped in the WinZip Fast format WILL run.
- Roms ziped in the WinZip Super Fast format WILL run.
- Roms ziped in the WinZip None format WILL run.

  
### Installation:   
Same process as with the AntSnes:  
1\. First Install Qt 4.6.3 binaries into your phone

- Nokia users can just download and install this : [ Qt 4.6.3 for S60 5th edition (24771 downloads) ](http://summeli.com/download/11294/ "Version 1")
- Samsung users: Download the Qt packages from[ http://www.olcso-tarhely.com/faenil/Qt\_4.7.3\_libs.zip](http://www.olcso-tarhely.com/faenil/Qt_4.7.3_libs.zip)
- Sony Ericsson users: You can get the official Qt installation package from: [ Qt 4.6.3 for SE devices (3274 downloads) ](http://summeli.com/download/11296/)

2\. Download the gpsp4symbian.sis  
3\. gpsp4Symbian requires the **SWEvent** capability. The SwEvent is required for key mapping: Now you can map call/end call etc. buttons for the gpsp usage. Therefore the following step is required to install the SW.  
Go to SymbianSigned and sign the AntSnesQt sis for your own phone IMEI.  
Step 1. Register to symbian signed [https://www.symbiansigned.com/ ](https://www.symbiansigned.com/) Gmail / Hotmail email adresses are banned from the symbian signed site, so you must use some other email service provider.  
Step 2. Sign the sis-file by yourself with the symbian signed web UI.

- Your Phone IMEI (you can obtain it digiting \*#06# on your phone)
- Your EMAIL Address (Nokia’s email address is working)
- gpsp4Symbian SIS Package

And then the symbiansigned should email you the signed gpsp4Symbianfor your phone. This package will be installable ONLY on your phone. This procedure works for all Symbian S60V5 Phones. I had also to change to date on the phone into yesterday to get it working..  
The alternative method is to hack your phone! You can find pretty good instructions from [MameXM download site.](https://sites.google.com/site/mamexm/Home/download-1-03) (scroll to the bottom of page: Signing &amp; Installing).  

### Download:   
Download the gpsp4Symbian: [ gpsp\_v065 (56818 downloads) ](/wp-content/uploads/downloads/2011/07/gpsp_065.sis)   
Sources are available on Github:[https://github.com/Summeli/gpSP4Cute/tree/S60\_5th\_edition](https://github.com/Summeli/gpSP4Cute/tree/S60_5th_edition)  

### The Bios:   
Remember to set the correct bios before loading ROMs. Make sure to get an authentic one , it’ll be exactly 16384 bytes large and should have the following md5sum “a860e8c0b6d573d191e4ec7db1b1e4f6”. The Bios extension should be .bin  
### Project Wiki page:    
[https://github.com/Summeli/gpSP4Cute/wiki](https://github.com/Summeli/gpSP4Cute/wiki) 

### Compatibility list:     
Compatibility list for S60 5th edition can be found at:  
[https://github.com/Summeli/gpSP4Cute/wiki/gpsp-for-S60-5th-edition-compatibility-list](https://github.com/Summeli/gpSP4Cute/wiki/gpsp-for-S60-5th-edition-compatibility-list)

### Read this before posting comments:   
- Do NOT Ask where to find ROMs / Bios. Asking about these will just get you banned!
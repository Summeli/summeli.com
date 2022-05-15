---
id: 1883
title: 'gpsp v. 0.6.1: Added support for Satio and Vivaz'
date: '2010-08-31T18:08:04+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1883'
permalink: /1883/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'S60 5th edition'
tags:
    - gpsp
    - satio
    - vivaz
---

the gpSP is a gameboy advance emulator originally written by Exophase. And now it’s ported to the Symbian OS!  
The newest update adds support for Sony Ericsson Satio and Vivaz. In all other ways it’s the same package as the 0.6 with experimental audio. The audio is pretty much behind from the action (sound lag), but it still can create quite nice mood for RPG-games.  

### How to get good audio:   
At least with some games it seems that the emulator can not buffer enough when the audio is set “ON” when loading a ROM. If the audio is clicking badly you should set the audio OFF and click continue. Now the emulator will have some time to buffer some audio 🙂 After a while you can switch the audio back into ON position again.

![](/jekyll-export//wp-content/uploads/2010/07/gpsp_051.jpg)

### What’s new 

- Experimental audio

### know issues:   

- not working on Symbian^3 based devices such as N8
- It’s a gpsp port, so see the gpsp compatibility list before complaining about non-working ROMs
- Audio is not yet implemented (I’m waiting for new Qt release with QAudio implementation)
- loading the state freezes the emulator in some games ( don’t worry, the batterysave still works)
- the emulator crashes if you try to load a ROM without setting the BIOS
- there are some limitations in the ZIP file support, so maybe you have to upzipt the ROMs
- The ZIP files seem to be eating quite a lot of RAM, so If ROM doesn’t work, try extracting it.
- Samsung blit fails when “keep aspect ratio” is ticked off
- The audio is quite much behind from the action

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

- Nokia users can just download and install this [Download Qt installation package](ftp://ftp.qt.nokia.com/pub/qt/symbian/4.6.3/qt_installer.sis)
- Samsung users: There’s really no official Qt installation package yet. You can get working Qt libraries by 
    1. installing wikitude i8910 version: <http://www.wikitude.org/>
    2. Check out [faenil’s QT installation instructions](http://i8910tuning.com/2010/07/22/welcome-to-i8910-qt/)
- Sony Ericsson users: You can get the official Qt installation package from:[ http://bit.ly/qt463demos](http://bit.ly/qt463demos)

[ ](ftp://ftp.qt.nokia.com/pub/qt/symbian/4.6.3/qt_installer.sis) 2. Download the gpsp4symbian.sis  
3\. gpsp4Symbian requires the **SWEvent** capability. The SwEvent is required for key mapping: Now you can map call/end call etc. buttons for the gpsp usage. Therefore the following step is required to install the SW.  
Go to SymbianSigned and sign the gpsp4Symbian.sis for your own phone IMEI  
using free Open Signed Online option <https://www.symbiansigned.com/app/page/public/openSignedOnline.do> this operation should be free of any charge.  
Read carefully the instructions on the SymbianSigned site.  
You must give them

- Your Phone IMEI (you can obtain it digiting \*#06# on your phone)
- Your EMAIL Address
- gpsp4Symbian SIS Package

And then the symbiansigned should email you the signed gpsp4Symbianfor your phone. This package will be installable ONLY on your phone. This procedure works for all Symbian S60V5 Phones. I had also to change to date on the phone into yesterday to get it working..  
The alternative method is to hack your phone! You can find pretty good instructions from [MameXM download site.](https://sites.google.com/site/mamexm/Home/download-1-03) (scroll to the bottom of page: Signing &amp; Installing).  


### Download:     
Download the gpsp4Symbian: [ gpsp4Symbian\_v0.6.1.sis (52803 downloads) ](/jekyll-export/wp-content/uploads/downloads/2010/08/gpsp_v06.sis)  
Sources are available on Github:[https://github.com/Summeli/gpSP4Cute/tree/S60\_5th\_edition](https://github.com/Summeli/gpSP4Cute/tree/S60_5th_edition)  

### The Bios:   
Remember to set the correct bios before loading ROMs. Make sure to get an authentic one , it’ll be exactly 16384 bytes large and should have the following md5sum “a860e8c0b6d573d191e4ec7db1b1e4f6”. The Bios extension should be .bin  

### Project Wiki page:   
<http://wiki.github.com/Summeli/gpSP4Symbian/>  
**Read this before posting comments:**

- Do NOT Ask where to find ROMs / Bios. Asking about these will just get you banned!
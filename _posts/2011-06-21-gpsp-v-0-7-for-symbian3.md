---
id: 2520
title: 'gpSP v. 0.7 for Symbian^3'
date: '2011-06-21T22:45:56+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2520'
permalink: /2520/
aktt_tweeted:
    - '1'
aktt_notify_twitter:
    - 'yes'
categories:
    - 'Symbian Anna'
    - Symbian^3
tags:
    - gpsp
---

the gpSP is a gameboy advance emulator originally written by Exophase. And now it’s ported to the Symbian OS!  
This version supports only Symbian^3 phones (N8, E7 etc.). The S60 5th edition users should use the older [gpsp 0.6.5 for S60 5th edition](/2557)  

### What’s new:   
- Support for Symbian^3
- Better Audio
- alpha channel for keys is now configured at video section (not in controls panel)
- 8-directional / 4 directional DPAD
- Hidden A+B button areas
- save/load states is now working

<iframe allowfullscreen="allowfullscreen" frameborder="0" height="315" loading="lazy" src="https://www.youtube.com/embed/eHtJpr0oKe0" width="560"></iframe>  
   
**Controls:**

- You can choose between 8-directional and 4-directional DPads.
- You can add hidden A+B button areas, to press both of them at once.

![](/wp-content/uploads/2011/06/gpsp-300x169.png)

  
### know issues:   

- **Mounted shares(Dropbox etc.) breaks the filemanger, so do not use mounted shares.**
- It’s a gpsp port, so see the gpsp compatibility list before complaining about non-working ROMs
- the emulator crashes if you try to load a ROM without setting the BIOS
- there are some limitations in the ZIP file support, so maybe you have to upzipt the ROMs
- The ZIP files seem to be eating quite a lot of RAM, so If ROM doesn’t work, try extracting it.
- Does not work on Nokia 500, since it doesn’t have GPU.

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
Just download and install. The installer contains a smartinstaller which will download and install Qt 4.7.3 for you if you don’t have it yet. The installer might take some time, so be patient 😉  

### Download:   
Download the gpsp4Symbian: [ gpsp\_v07\_for\_symbian^3 (58652 downloads) ](/wp-content/uploads/downloads/2011/09/gpsp_v071.sis)  
Sources are available on Github: <https://github.com/Summeli/gpSP4Cute>  

### The Bios:   
Remember to set the correct bios before loading ROMs. Make sure to get an authentic one , it’ll be exactly 16384 bytes large and should have the following md5sum “a860e8c0b6d573d191e4ec7db1b1e4f6”. The Bios extension should be .bin  

### Project Wiki page:   
[https://github.com/Summeli/gpSP4Cute/wiki](https://github.com/Summeli/gpSP4Cute/wiki)

### Compatibility list:**  
Compatibility list for Symbian^3 can be found at:  
[https://github.com/Summeli/gpSP4Cute/wiki/gpSP-for-Symbian%5E3-compatibility-list](https://github.com/Summeli/gpSP4Cute/wiki/gpSP-for-Symbian%5E3-compatibility-list)

### Read this before posting comments:**
- Do NOT Ask where to find ROMs / Bios. Asking about these will just get you banned!
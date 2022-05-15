---
id: 4508
title: 'gpSP 0.7.2+ Repacked with new game_config'
date: '2013-07-04T08:41:12+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=4508'
permalink: /4508/
categories:
    - 'Symbian Belle'
tags:
    - gpsp
---

the gpSP is a gameboy advance emulator originally written by Exophase. And now it’s ported to the Symbian OS!  
I head from the users that the game\_config.txt from the past works better than the one packaged with 0.7.2. Some say that the Pokemon Fire Red works with this game\_config, while it doesn’t work with the one packages in 0.7.2. For me it seems to be working with both game\_configs, so I decided to make a new package for you. Does this one work better, do we have better game compatibility, or do you prefer the one packaged with the older 0.7.2? You can reply in the comments section.  
This version supports only Symbian^3 phones with Symbian Belle refresh installed (N8, E7 etc.). The old Symbian Anna users should still use the older [gpSP 0.7.](/2520) The S60 5th edition users should use the [gpsp 0.6.5 for S60 5th edition](/4495)  

### What’s new:   

- Repacked with new game\_config.txt

<iframe allowfullscreen="allowfullscreen" frameborder="0" height="315" loading="lazy" src="https://www.youtube.com/embed/yXTpnRt0WfY" width="560"></iframe>  
   
### Controls:

- You can choose between 8-directional and 4-directional DPads.
- You can add hidden A+B button areas, to press both of them at once.

![](/wp-content/uploads/2011/06/gpsp-300x169.png)   
gpsp: the red dots indicates the hidden A+B areas

### know issues:    

- **Mounted shares(Dropbox etc.) breaks the filemanger, so do not use mounted shares.**
- It’s a gpsp port, so see the gpsp compatibility list before complaining about non-working ROMs
- the emulator crashes if you try to load a ROM without setting the BIOS
- there are some limitations in the ZIP file support, so maybe you have to upzipt the ROMs
- The ZIP files seem to be eating quite a lot of RAM, so If ROM doesn’t work, try extracting it.

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
Just download and install.  

### Download:   
Download the new 0.7.2+ version: [ gpsp\_072\_repacked (15958 downloads) ](/wp-content/uploads/downloads/2013/07/gpsp_v072_repacked.sis)  
or if you prefer the older version, you can try it too: [ gpsp\_v0.72 (24132 downloads) ](/wp-content/uploads/downloads/2012/09/gpsp_v072.sis)  

Sources are available on Github: <https://github.com/Summeli/gpSP4Cute>  

### The Bios:   
Remember to set the correct bios before loading ROMs. Make sure to get an authentic one , it’ll be exactly 16384 bytes large and should have the following md5sum “a860e8c0b6d573d191e4ec7db1b1e4f6”. The Bios extension should be .bin  

### Project Wiki page:   
<https://github.com/Summeli/gpSP4Cute/wiki>  

### Compatibility list:   
Compatibility list for Symbian^3 can be found at:  
<https://github.com/Summeli/gpSP4Cute/wiki/gpSP-for-Symbian%5E3-compatibility-list>   

### Read this before posting comments:    

- Do NOT Ask where to find ROMs / Bios. Asking about these will just get you banned!
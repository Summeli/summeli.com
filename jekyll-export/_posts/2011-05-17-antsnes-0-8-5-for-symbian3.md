---
id: 2453
title: 'AntSnes 0.8.5 for Symbian^3'
date: '2011-05-17T16:48:55+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2453'
permalink: /2453/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - Symbian^3
tags:
    - AntSnes
    - N8
---

AtnSnes is Snes9x emulator for Symbian. It is actually based on [DrPocketSNES](http://reesy.gp32x.de/DrPocketSnes.html "DrPocketSNES") version 6.4.4, which in turn is based on snes9x 1.39  
The new AntSnes comes with multitouch and with new transparent keys. You’ll need a Symbian^3 based phone to run this (N8, C7, E7 etc..). The old S60 5th edition is not supported by this version anymore. S60 5th edition users should use [AntSnesQt 0.7](/2386)  

### What’s new   

- You can now adjust the alpha channel for keys
- alpha channel for keys is now configured at video section (not in controls panel)
- Multiple blit options (fullscreen &amp; keep aspect ratio) (see video settings)
- You can map multiple snes-keys into one button
- The emulation is now stopped when the app goes into background, so it won’t drain your battery even if you forget it on.
- Fine tuned the onscreen buttons a bit. I think that they work a bit better now…
- standalone package removed

### Known issues:   

- Mounted shares(Dropbox etc.) breaks the filemanger, so do not use mounted shares.
- The volume control slider works only if you drag it into new position (tapping a new level doesn’t work)

<iframe allowfullscreen="allowfullscreen" frameborder="0" height="315" loading="lazy" src="https://www.youtube.com/embed/eHtJpr0oKe0" width="560"></iframe>  
**Installation:**  
Just download and install. The installer contains a smartinstaller which will download and install Qt 4.7.3 for you if you don’t have it yet.  
  
**Download:**  
Download the AntSnes 0.8.5 with the smart-installer: [ AntSnes v 0.8.5 (18429 downloads) ](/jekyll-export/wp-content/uploads/dlm_uploads/2018/01/AntSnes_v085.sis)  
Sources are available on Github: <http://github.com/Summeli/AntSnes>  

### Read this before posting comments:   

- Do NOT Ask where to find ROMs / Bios. Asking about these will just get you banned!
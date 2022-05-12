---
id: 209
title: 'AntSnes release 0.2 : Support for all 3rd edition phones'
date: '2009-01-30T22:39:16+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=209'
permalink: /209/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
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

The new AntSnes release 0.2 is ready. The current release 0.2 supports most S60 3rd edition phones. It’s currently tested with N73(3.0), N95(3.1) and N96(3.2). The new package also adds new settings view, which can be used for configuring the emulator for different devices.  
**Antsnes 0.2:**  
Download the sis: [antsnes\_v02](/jekyll-export/wp-content/uploads/2009/01/antsnes_v02.sis)  
source: [antsnes\_v02\_src.zip](/jekyll-export/wp-content/uploads/2009/01/antsnes_v02_src.zip)  
  
**Installation:**

1. Install P.I.P.S 1.3(or later if available) to the phone (pips\_nokia\_1\_3\_SS.sis).  
    You will probably find this file faster by googling it, but if you’re out of luck, you can extract it from official nokia plugin, which can be donwloaded from [forum.nokia](http://www.forum.nokia.com/info/sw.nokia.com/id/91d89929-fb8c-4d66-bea0-227e42df9053/Open_C_SDK_Plug-In.html#http://www.forum.nokia.com/info/sw.nokia.com/id/91d89929-fb8c-4d66-bea0-227e42df9053/Open_C_SDK_Plug-In.html). This step is not required for all S60 3rd edition phones, so you can also try to skip this phase.
2. Install AntSnes.
3. Enjoy


### AntSnes settings:
There is two different graphic modes, the n-gage mode and portrait. The portrait mode is the default. It’s meant for most 3rd edition phones(phones without “n-gage mode”). The orientation modification takes effect, when AntSnes is started next time( a restart required).  
The N-gage mode is meant for phones with “n-gage mode” like N95 and N96. The N96 can use the multimediakeys by default, but N95 users must use [Magic keys](http://www.symbian-freak.com/downloads/freeware/cat_s60_3rd/descriptions/systools/magic_keys_remap_and_extend_your_keyboard.htm) to map keys 1-4 to multimediakeys.

[N96 keymap](/jekyll-export/wp-content/uploads/2009/01/n96_keys-300x198.jpg)

### Key config**  
Start key config to configure keys. The multimediakeys are not supported in the key config, but you can use any normal keys in here.  

### Known limitations:

- The AntSnes is based on GP32’s version of assembly optimized snes9x. It has a lot of tweaks for better performance, and therefore not all games are working. I’m not planning to add any additional support for other games in this release. The AntSnes is just another port of this very well optimized emulator.
- The sound support is missing. I have spend a lot of time for the sound support, and the biggest problem is that it requires too much processing power. I honestly don’t think that it will be possible with ARM9 based S60 devices like N73 or N96. It might be possible with N95, if some graphic layers are disabled.
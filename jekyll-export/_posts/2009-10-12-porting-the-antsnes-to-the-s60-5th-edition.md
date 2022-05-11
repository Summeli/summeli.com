---
id: 1311
title: 'Porting The AntSnes to the S60 5th edition'
date: '2009-10-12T20:19:44+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1311'
permalink: /1311/
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
aktt_tweeted:
    - '1'
categories:
    - Video
tags:
    - AntSnes
    - n97
    - S60
---

I have been porting the AntSnes to the 5th edition. The reason I have been a bit lazy is that I can’t get the TRK debugger working with N97. So I have been working only with filelogger. That sucks!  
Here’s some video of the current state of the AntSnes to the 5th edition. I’m running only the regular c-core in the video, so the final version could be a bit faster with the asm-optimized emulator core. I just can’t get the previous asm-optimized core from 3rd edition to work with the S60 5th edition for some reason, and I’m too lazy to add all loggings to all sources.. Hopefully the next N97 firmware will help to my debugger problem.  
<iframe allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="315" loading="lazy" src="https://www.youtube.com/embed/tM3liXWTbbM" width="560"></iframe>  
As you can see from the video I can run and jump at the same time, so it really does support 3 buttons at the same time, if the phone is capable of it (nice feature for chrono trigger).  
You might notice that I didn’t use menu to load the ROM, and the reason is that I can’t do it yet. The current version has some issues with the menus on the 5th edition that needs to be solved before I can really release the 5th edition version. But as you can see, I’m getting there 🙂  
**Update:**  
The menu problems are now solved. There’s only some small tasks before this emu is ready for you guys 🙂
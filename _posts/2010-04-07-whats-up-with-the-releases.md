---
id: 1584
title: 'What&#8217;s up with the releases'
date: '2010-04-07T22:41:58+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1584'
permalink: /1584/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - AntSnes
    - gpsp
    - psx4all
    - psx4symbian
    - symbian^3
---

This blog has been pretty quiet lately, and maybe you’re wondering why there has been no releases lateley 🙂 Well, I have been snowboarding the last month, so I really haven’t made any progress. I still have a lot of photo’s and videos to edit, which will keep me away from my emulator projects for a while.. But soon the releases will be coming at the usual speed 🙂

![](/wp-content/uploads/2010/04/snowboarding1-300x250.jpg)

As I said earlier the future of my emulators is in the Qt. The works is proceeding really well. The AntSnesQt is only missing style sheet, and then I could release it. Actually I already have started the gpsp port with the same Qt based UI. The gpsp requires few SDL-alike functions to be mapped into the UI, but I can mostly reuse the stuff I made for the AntSnes.  

I haven’t abandoned the psx4symbian port, but I’m really not working on it neither. The proof of concept was made in couple of hours after the gpsp port, and my plan is to reuse all the gpsp stuff again to make that one. This should be quite fast to thing to do after I have the gpsp running on Qt.  

Why not to make the psx4all port at first, and then work with gpsp and AntSnes? The psx4all video has already over 10 000 views on youtube, and it seems like a pretty popular project. My reasoning here is that I don’t believe that current S60 5th edition phones could emulate the psx4all with decent speed. There’s no technical issued preventing you to run the upcoming psx4all port with current 5th edition phones too, but my personal goal is to run the psx4all with Symbian^3 phones.  
  
The Symbian^3 phones will be a lot better for gaming/emulation because of the new graphics architecture (NGA) . The basic idea in the NGA is that now you can draw into the screen more directly and with graphic accelerations (opengl es 2.0, openvg, etc.) . See the graphics architecture evolution in Symbian wiki page: [http://developer.symbian.org/wiki/index.php/Graphics/Component\_Architecture\_Evolution](http://developer.symbian.org/wiki/index.php/Graphics/Component_Architecture_Evolution). I expect that with the new graphics architecture The AntSnes and the gpsp emulator should be able to run at full speed (60 fps). This would also give a huge performance boost for the psx4all 🙂  
Here’s a summary how I’m planning to proceed with my emulators projects.

![](/wp-content/uploads/2010/04/rel_plan.jpeg)
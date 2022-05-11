---
id: 1001
title: 'MinGW Symbian OS Build Chain: Debugging'
date: '2009-07-28T19:40:43+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1001'
permalink: /1001/
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
aktt_tweeted:
    - '1'
categories:
    - 'MinGW buidchain'
    - 'Symbian Development'
tags:
    - Debugging
    - GCCE
    - gpsp
    - MinGW
    - msys
---

I have been developing the MinGW build chain to make the embedded open source porting easier since last spring. Now after my holidays I had some time to develop it even further. I added debugging with Carbide and TRK to the build system.  
At first we have are going to need to symbol files for debuggin. This is actually quite easy. Just add “-g” for the compiler, and it will compile a debug version. Then the linker will produce the .exe file with the symbols. A funny thing is that the Symbian OS Post-linker elf2e32 will rip off all debug symbols, so we have to make a copy from that executable before that. The symbol file is actually the pure .exe before the evil Symbian OS post-linker put it hands on it.  
The next step is to copy .sym .exe and .map files under EPOC32\\release\\GCCE\\UDEB folder so the Carbide can use them for debugging.  
Here is the updated Makefile for debug support: [Makefile](http://www.summeli.com/wp-content/uploads/2009/07/Makefile)  
You have to be able to take the source files into your workspace in carbide, so you have to make a standard Symbian OS project from them. It does not have to compile, we just need to get the files into the workspace. Just make a standard bld.inf file and mmp-file where you list all the source files for the project.  
We are not going to build the project so we have to undo the building. Go to Window &gt; Preferences &gt; Run/Debug &gt; Launching  
and then untick “Build (if required) before launching”.

<div class="wp-caption aligncenter" id="attachment_1006" style="width: 310px">[![carbide_nobuild](http://www.summeli.com/wp-content/uploads/2009/07/carbide_nobuild-300x270.jpg "carbide_nobuild")](http://www.summeli.com/wp-content/uploads/2009/07/carbide_nobuild.jpeg)untick "Build (if required) before launching".

</div>  
Then just right click the project and select Debug as -&gt; Debug Configurations and configure the TRK and debugging stuff as you usually do. Then go into the Executables tab and select “Executables selected below” in “Load symbols for these executables and target them for debugging”. Now click add and find you executable under epoc32\\release\\gcce\\udeb folder and start debugging with TRK.  
This was a very nice exercise for my gpsp porting attempt. I still can’t be sure that if I got it any further, but with debugger I might be able to pinpoint some of my problems and look for the answers.  
I’m planning to merge all of this MinGW buildchain stuff in one complete tutorial. It’ll probably happen when I have had enough gpsp debuggin 🙂 
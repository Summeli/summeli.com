---
id: 2794
title: 'How did my native code experiment go with wp7'
date: '2012-04-24T14:59:48+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2794'
permalink: /2794/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Dev Talk'
tags:
    - wp7
---

I have been pretty much spending all my free time during the winter for snowboarding and ice climbing. Now that the winter is nearly over at northern Europe, I got some time to come back to my hacking hobby. This is also to remind me how did my wp7 experiments go, if I want to come back to this stuff at some point.  
**Native code**  
At January I got the native snes9x library build and I was even able to call it from the managed code side. The native code usage has been well documented by XDA developer [Heathcliff74](http://forum.xda-developers.com/member.php?u=3254428) <http://forum.xda-developers.com/showthread.php?t=1299134>  
What was strange that on January I didn’t need the ID\_CAP\_INTEROPSERVICES capability to my application, it worked anyway. I guess that Nokia had some bugs in their first Mango firmware to allow native code without proper capabilities. Yesterday I got back with the code, and I noticed that I can not run the code anymore without the capability.  
**Callbacks from the native code to the managed code**  
My biggest problem back then was that I could call LoadROM function from the managed code side, but I didn’t have any tools to debug what went wrong in the native side, so I couldn’t figure out what went wrong after calling the loadROM. My first idea was to set up debug callbacks into the managed code side that I could still call from the native side like

```
<pre class="brush: cpp; title: ; notranslate" title="">
void DEBUG(string debugMessage){
console.debug(debugMessage)
}
```

But I newer found a way to a way how to do this. So I’m really stuck with this one without any plans to continue. I might get back to this if someone finds some ways of making the callbacks, or debugging the native code.  
**InteropUnlock**  
Currently Nokia devs can hack their Lumias, to get full control, and the InteropUnlock is available, if you like to continue native development. Thanks to XDA-developer [suzughia](http://forum.xda-developers.com/member.php?u=4584802) <http://forum.xda-developers.com/showthread.php?t=1599401>  
  
**What’s next**   
I guess that I’ll be coming back to the windows phone when the wp8 is available, since it should have the native code support build in, and I don’t need to use 10 years old ARMV4 architecture and lots of hacks to run native code on it.  
I have some really cool ideas what I want to try on Meego. I’ll share the progress with you again, if I ever get anywhere with the new stuff.
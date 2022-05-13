---
id: 3006
title: 'Changes in Symbian Memory Management in Belle FP1 and Belle Refresh'
date: '2012-10-10T08:30:50+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=3006'
permalink: /3006/
aktt_notify_twitter:
    - 'no'
categories:
    - 'Dev Talk'
    - 'Symbian Development'
tags:
    - belle
---

A while a go I made [gpsp update for the Symbian Belle and Belle Refresh](/2991). I learned that for some reason Nokia has changed the memory management a bit, so the new Symbian version will fail when I’m creating my own heaps with RHeap API’s. It seems that the new Symbian is unable to increase the application heap size when creating new heaps. Luckily the fix is rather easy;  
I just had to increase the initial amount of Heap reserved by the app startup by increasing the target.EPOCHEAPSIZE in the Qt’s .pro file. like this:

```
//it was somethign small like: symbian:TARGET.EPOCHEAPSIZE = 0x200000 0x1000000
symbian:TARGET.EPOCHEAPSIZE = 0x800000 0x1400000
```

Personally I have no idea why Nokia made any changes to the Symbian kernel at this point, when they have pretty much killed the whole platform. They are just getting broken apps for dying ecosystem. If I wouldn’t have had the Symbian SDK still installed, I wouldn’t have bothered to download the SDK again just to make even a minor update.
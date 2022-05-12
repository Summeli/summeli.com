---
id: 1457
title: 'Implementing AntSnes with Qt part 5: Implementing the Blit'
date: '2010-03-03T19:15:40+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1457'
permalink: /1457/
aktt_tweeted:
    - '1'
aktt_notify_twitter:
    - 'yes'
categories:
    - 'Qt Development'
    - 'Symbian Development'
tags:
    - AntSnesQtDev
    - 'Qt Development'
---

The current Qt version is implemented on top of the old Avkon layer, and it really doesn’t have fast blitting methods available. Therefore I Implemented the blit with Symbian’s Anti-Tearing API, which should be the fastest available method to draw on the screen. Forum.nokia has a very good example how to use the [Anti-tearing API](http://wiki.forum.nokia.com/index.php/Anti-tearing_with_CDirectScreenBitmap).  
There’s a ton of Qt blog posts about graphics performance, so I’m not going though all that stuff again. Here’s one really good post about the performance:[ http://labs.trolltech.com/blogs/2009/12/16/qt-graphics-and-performance-an-overview/](http://labs.trolltech.com/blogs/2009/12/16/qt-graphics-and-performance-an-overview/) I’ll make an update for the fast blit, when there’s real hardware acceleration for Qt in Symbian available, so I can make some benchmarking as well. Until then I’m going with the Anti-Tearing API.  
For the blitting I’m using the scaling function I described in the my earlier blog post [fast image scaling](http://www.summeli.com/?p=1227). The render function is implemented as Qt slot, so I can call it from another thread, see also my post about the [worker thread](/1475).  
Here’s the rendering function.

```
void QBlitterWidget::render()
 {
 if (IsActive())
    {
     Cancel();
    }
 TAcceleratedBitmapInfo bitmapInfo;
 iDSBitmap->BeginUpdate(bitmapInfo);
 bitmapdata = (TUint8*) bitmapInfo.iAddress;
 //blit the data
 bitmapBlit( g_screenptr, bitmapInfo.iAddress);
 iDSBitmap->EndUpdate(iStatus);
 SetActive();
 }
```
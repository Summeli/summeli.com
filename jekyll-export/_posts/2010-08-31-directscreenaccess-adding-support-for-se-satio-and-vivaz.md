---
id: 1875
title: 'DirectScreenAccess: Adding support for SE Satio and Vivaz'
date: '2010-08-31T17:58:36+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1875'
permalink: /1875/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - satio
    - vivaz
---

I got quite many complaints about gpsp crashing with Sony Ericsson Satio and Vivaz. I didn’t have any clue what’s wrong with gpsp, until I found this thread in the SE Support forums. <http://developer.sonyericsson.com/community/thread/50103>  
It turns out that the Sony Ericsson Satio and Vivaz seems to have similar issues with the Blit as Samsung i8910 with a twist: The Sony Ericsson phones just crashes when creating a CDirectScreenBitmap in different size than (0,0,360,640). We are in luck here, since I already have a [blit fix](http://www.summeli.com/?p=1800) that I can re-used for SE phones too!  
The SE support also says that the ScreenDevice-&gt;update() must be called before the screen is actually updated. Therefore we must add that into the blit method.

```
<pre class="brush: cpp; title: ; notranslate" title="">
    TAcceleratedBitmapInfo bitmapInfo;
    iDSBitmap->BeginUpdate(bitmapInfo);
    bitmapdata = (TUint8*) bitmapInfo.iAddress;
    bitmapBlit( (TUint8*) g_screenptr, bitmapdata);
    iDSBitmap->EndUpdate(iStatus);
    SetActive();
  iDirectScreenAccess->ScreenDevice()->Update(); <-- Added this line to make the drawing visible!
```

The update command is also required for Symbian^3 based devices, see the [DSA Migration guide in forum.nokia](http://library.forum.nokia.com/index.jsp?topic=/Nokia_Symbian3_Developers_Library/GUID-3F0FCBB5-98D2-4355-96E3-2DA938DE1C16.html). So this update might also give Symbian^3 support for the gpsp 🙂
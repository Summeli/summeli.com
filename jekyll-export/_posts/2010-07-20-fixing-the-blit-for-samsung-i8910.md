---
id: 1800
title: 'Fixing the blit for Samsung i8910'
date: '2010-07-20T19:01:54+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1800'
permalink: /1800/
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - i8910
    - Samsung
    - scaling
    - Symbian
---

I got lot’s of complaints about the broken blit in gpsp4Symbian with Samsung i8910.  
The root cause for this problem is that the following code doesn’t set the ScreenBuffer in samsung into Landscape orientation, while it does work just fine on Nokia’s phones. I heard that there are some other Qt applications ( at least AntSnesQt 😉 that have the same problem, so I felt this worth of sharing.

```
    CAknAppUi* appUi = dynamic_cast<CAknAppUi*> (CEikonEnv::Static()->AppUi());
    TRAPD(error,
    if (appUi) {
     // Lock application orientation into landscape
     appUi->SetOrientationL(CAknAppUi::EAppUiOrientationLandscape);
     appUi->SetKeyEventFlags(CAknAppUi::EDisableSendKeyShort|CAknAppUi::EDisableSendKeyLong);
    }
```

The screen is still in portrait mode, and therefore it looks like this:

![](/jekyll-export/wp-content/uploads/2010/07/rotated.jpg)

rotated screen with samsung

Fixing the blit comes in two phases:  
  
First you must fix the coordinates of the DirectScreenBitmap ( the coordinates are different in landscape/portait mode) 

```
	iDSBitmap->Create(
                // This is an easy case: just change places of x and y coordinates.
                // in most cases you'll have to calculate these values by yourself
		//TRect(160,0,640,360), CDirectScreenBitmap::EDoubleBuffer);
		   TRect(0,160,360,640), CDirectScreenBitmap::EDoubleBuffer);
```

After this you must write the pixels into the bitmap in modified order. The Samsung framebuffer is illustrated on below.

![](/jekyll-export/wp-content/uploads/2010/07/filling_framebuffer1.jpg)   
filling the framebuffer

Since the bitmap is orientated in different position the distance between the black and red pixels is 320 pixels. Therefore the buffer should be filled like this:

```
for( TInt i=0; i<240; i++)
{
copyPixel16MU( bitmap, screen );
bitmap += 320;
//simple interpolation from 240 into 480 pixels, each pixel is just actually copied twice
copyPixel16MU( bitmap, screen );
bitmap += 320;
screen++;
}
```

There’s a minor fix coming to gpsp in few days with fixed blit for Samsung i8910 (I fixed only the “keep aspect ratio” mode). This fix was debugged by email with [faenil ](http://www.i8910tuning.com)(thanks again faenil, you have been a great help in here): I sent away a sis file, and received a photo of the screen 🙂 This way of developing it further is too time consuming for me, and I’m hoping that someone with Samsung phone could continue fixing these blits 🙂  
I don’t want to scare anyone away with my [mingw build](/1274), so I decided to share the gpsp static libarary file that is required to build the gpsp4symbian  
here’s gpsp debug binaries. Just copy them into epoc32\\release\\armv5\\udeb

- [http://dl.dropbox.com/u/2936915/gpsp/gpsp\_debug/gpSP4Symbian.LIB](http://dl.dropbox.com/u/2936915/gpsp/gpsp_debug/gpSP4Symbian.LIB)
- [http://dl.dropbox.com/u/2936915/gpsp/gpsp\_debug/gpSP4Symbian.LIB.map](http://dl.dropbox.com/u/2936915/gpsp/gpsp_debug/gpSP4Symbian.LIB.map)

And here’s the release binary of that lib: copy it into epoc32\\release\\armv5\\urel

- [http://dl.dropbox.com/u/2936915/gpsp/gpsp\_release/gpsp4symbian.LIB](http://dl.dropbox.com/u/2936915/gpsp/gpsp_release/gpsp4symbian.LIB)
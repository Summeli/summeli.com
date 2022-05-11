---
id: 1227
title: 'Fast image scaling with multiplier between 1-2'
date: '2009-09-25T17:30:19+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1227'
permalink: /1227/
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - interpolate
    - porting
    - scaling
---

I made a simple scaling function for gpsp4symbian to stretch the frames into full screen. The algorithm seems to be working quite well with scaling factors between 1-2. Thanks to [AnotherGuest](http://anotherguest.se) for tips.  
In this example 1.3 scaling factor is used for vertical scaling and 1.5 for horizontal scaling.  
Fist let’s make the scaling tables.

```
<pre class="brush: cpp; title: ; notranslate" title="">
void symb_create_interpolate_table()
  {
  TReal j = 1.33; //horizontal
  TReal loop = 0;
  TReal real_temp;
  for( TInt i=0; i<240; i++)
    {
    real_temp = i*j + 0.5;
    interptable_w[i] = real_temp;
    }
  j= 1.5; //vertical
  for( TInt i=0; i<160; i++)
    {
    real_temp = i*j + 0.5;
    interptable_h[i] = real_temp;
    }
  }
```

Then we can use the pre-calculated tables to determinate if we have to interpolate a pixel or a line or not. There are all kinds of nice interpolation algorithms for images, but in this example I just reproduced the pixels for the speed. In theory we should also do some filtering after the interpolation, but that’s also abandoned for the speed.

```
<pre class="brush: cpp; title: ; notranslate" title="">
u16 *screenlarge_ptr = large_ptr;
u16 *screengba_ptr = small_ptr;
u8 i=0;
u8 j =0;
u16 t1;
u16 t2;
u16 stop;
for(j=0; j<160;j++)
 {
 for( i=0; i<240; i++)
   {
   *screenlarge_ptr = *screengba_ptr;
   if( interptable_w[i] != (interptable_w[i+1] -1) )
     {
     //interpolate, or reproduce the pixel
     screenlarge_ptr++;
     *screenlarge_ptr = *screengba_ptr;
      }
   screengba_ptr++;
   screenlarge_ptr++;
   }
 if( interptable_h[j] != (interptable_h[j+1] -1))
   {
   //copy whole previous line
   screen_temp = screenlarge_ptr - 320;
   memcpy(screenlarge_ptr, screen_temp, 320*2);
   screenlarge_ptr +=  320;
   }
 }
```
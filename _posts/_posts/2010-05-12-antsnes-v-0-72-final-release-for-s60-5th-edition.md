---
id: 1699
title: 'AntSnes v. 0.72: final release for S60 5th edition'
date: '2010-05-12T22:24:04+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1699'
permalink: /1699/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'S60 5th edition'
    - Symbian^3
tags:
    - AntSnes
---

I decided to make one more release for the 5th edition since the Qt + SwEvent is only working on Nokia’s phones. I’ll be using Qt from now on, and I recommend all Nokia users to take the Qt version, not this one.  
Thanks for Saiyaku for the new D-pad graphics.  

### What’s new

- Improved compatibility? (the code is much better aligned with drPocketSnes)
- In this update the d-pad is now optimized for resistive screen, and the red/green/menu buttons can be mapped as buttons in the key config digalog.

![](/jekyll-export//wp-content/uploads/2010/05/largeDPad.jpg)


**know issues:**- 
- Audio isn’t working
- PAL ROMs do not work
- It’s final realease without Qt

  
### Installation:     
1\. Download the AntSnes.sis  
2\. The AntSnes requires the **SWEvent** capability. The SwEvent is required for key mapping: Now you can map call/end call etc. buttons for the AntSnes usage. Therefore a new step is required to install the SW.  
Go to SymbianSigned and sign the AntSnesQt sis for your own phone IMEI  
using free Open Signed Online option <https://www.symbiansigned.com/app/page/public/openSignedOnline.do> this operation should be free of any charge.  
Read carefully the instructions on the SymbianSigned site.  
You must give them

- Your Phone IMEI (you can obtain it digiting \*#06# on your phone)
- Your EMAIL Address
- AntSnesQt SIS Package

And then the symbiansigned should email you the signed AntSnes for your phone. This package will be installable ONLY on your phone. This procedure works for all Symbian S60V5 Phones.  
The alternative method is to hack your phone! You can find pretty good instructions from [MameXM download site.](https://sites.google.com/site/mamexm/Home/download-1-03) (scroll to the bottom of page: Signing &amp; Installing).  
\[ad\]  
**Download:**  
Download the AntSnesQt: [ AntSnes\_V072 (29716 downloads) ](/jekyll-export/wp-content/uploads/downloads/2010/05/AntSnes_v072.sis)  
Sources are available on Github: <http://github.com/Summeli/AntSnes>
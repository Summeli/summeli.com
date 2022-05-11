---
id: 1685
title: 'AntSnesQt V. 0.6: new graphics'
date: '2010-05-12T22:26:00+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1685'
permalink: /1685/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'S60 5th edition'
tags:
    - AntSnes
---

The new AntSnesQt comes with Big D-pad, which is optimized for resistive touchscreen.  
I had some help for the new graphics for this release:

- Thanks for Saiyaku for the new D-pad graphics and UI graphics.
- Thaks for Jasper Terveer for the small d-pad and button graphics.

**What’s new**

- Improved compatibility? (the code is much better aligned with drPocketSnes)
- Big D-PAD
- The new AntSnes has more realistic snes style graphics. See it yourself

<div class="wp-caption aligncenter" id="attachment_1694" style="width: 394px">[![](http://www.summeli.com/wp-content/uploads/2010/05/mainscreen.jpg "mainscreen")](http://www.summeli.com/wp-content/uploads/2010/05/mainscreen.jpg)AntSnesQt main screen

</div><div class="wp-caption aligncenter" id="attachment_1697" style="width: 394px">[![](http://www.summeli.com/wp-content/uploads/2010/05/largeDPad.jpg "largeDPad")](http://www.summeli.com/wp-content/uploads/2010/05/largeDPad.jpg)The Big D-Pad

</div><div class="wp-caption aligncenter" id="attachment_1690" style="width: 394px">[![](http://www.summeli.com/wp-content/uploads/2010/05/newbuttons.png "newbuttons")](http://www.summeli.com/wp-content/uploads/2010/05/newbuttons.png)New buttons

</div>  
  
**Know issues:**- Audio isn’t implemented
- Qt with SwEvent works only on Nokia phones, other S60 users should use[ the AntSnes 0.72.](http://www.summeli.com/?p=1699)
- PAL ROMs do not work

**Installation:**  
1\. First Install Qt 4.6.2 binaries into your phone: [Download Qt installation package](ftp://ftp.qt.nokia.com/pub/qt/symbian/4.6.2/qt_installer.sis)  
2\. Download the AntSnesQt.sis  
3\. AntSnesQt requires the **SWEvent** capability. The SwEvent is required for key mapping: Now you can map call/end call etc. buttons for the AntSnes usage. Therefore a new step is required to install the SW.  
Go to SymbianSigned and sign the AntSnesQt sis for your own phone IMEI  
using free Open Signed Online option <https://www.symbiansigned.com/app/page/public/openSignedOnline.do> this operation should be free of any charge.  
Read carefully the instructions on the SymbianSigned site.  
You must give them

- Your Phone IMEI (you can obtain it digiting \*#06# on your phone)
- Your EMAIL Address
- AntSnesQt SIS Package

And then the symbiansigned should email you the signed AntSnesQt for your phone. This package will be installable ONLY on your phone. This procedure works for all Symbian S60V5 Phones.  
The alternative method is to hack your phone! You can find pretty good instructions from [MameXM download site.](https://sites.google.com/site/mamexm/Home/download-1-03) (scroll to the bottom of page: Signing &amp; Installing).  
\[ad\]  
**Download:**  
Download the AntSnesQt: [ AntSnesQt\_v06 (38978 downloads) ](http://summeli.com/download/11258/ "Version 0.6")  
Sources are available on Github: <http://github.com/Summeli/AntSnes>
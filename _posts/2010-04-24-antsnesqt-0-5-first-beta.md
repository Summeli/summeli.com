---
id: 1604
title: 'AntSnesQt 0.5 : first beta'
date: '2010-04-24T00:10:27+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1604'
permalink: /1604/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'S60 5th edition'
tags:
    - AntSnes
---

The AntSnes Qt is ready for first testing round. The whole UI is now working on top of Qt, so I expect there to be some new bugs compared to the older AntSnes version. The good news is that this installation won’t overwrite the older AntSnes. I also heard the the D-pad doesn’t suck anymore, so you should be able to use this emu with touch only phones too.  
I didn’t even try to get the Audio working, since the QAudio is not yet working in the Qt 4.6.2. I’ll continue with that after the QAudio is finalized by Nokia.  
![](/wp-content/uploads/2010/04/antsnes_with_style-300x168.jpg)  

### Know issues:   
1\. The audio is not yet implemented.  
2\. Save states are now found in different slots than in the previous AntSnes release.  
3\. The installation is now a bit more complicated, since the **SWEvent** capability is required.  
  
### Installation:*  
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
s
### Download:   
Download the AntSnesQt: [ AntSnesQt\_v05 (3529 downloads) ](/wp-content/uploads/downloads/2010/04/AntSnesQt_v05.sis)  
Sources are available on Github: <http://github.com/Summeli/AntSnes>
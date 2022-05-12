---
id: 2277
title: 'Building Symbian Projects with QtSDK'
date: '2011-04-13T16:54:03+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2277'
permalink: /2277/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Qt Development'
    - 'Symbian Development'
tags:
    - mmp
    - QtSDK
    - Symbian
---

All new Symbian SDKs are now distributed inside the new QtSDK, so that should be my primary build environment. The new QtSDK also includes an updated version of GCCE (4.x), and new sbsv2 build, which is a lot better than the old symbian abld-build. With this tutorial you can still build your old symbian projects from mmp-files.  

### Configuring the new sbsv2 build to the QtSDK    
Here’s an example of my setEnv.bat. In this case the QtSDK was installed into c-drive

```
SET PATH=C:\QtSDK\Symbian\tools\sbs\bin;C:\QtSDK\Symbian\tools\perl\bin;C:\QtSDK\Symbian\SDKs\Symbian3Qt473\epoc32\gcc\bin;C:\QtSDK\Symbian\SDKs\Symbian3Qt473\epoc32\tools;%PATH%
SET EPOCROOT=\QtSDK\Symbian\SDKs\Symbian3Qt473\
SET SBS_MINGW=C:\QtSDK\Symbian\tools\sbs\win32\mingw
SET SBS_HOME=C:\QtSDK\Symbian\tools\sbs
SET SBS_GCCE441BIN=C:\QtSDK\Symbian\tools\gcce4\bin
call C:\QtSDK\Symbian\SDKs\Symbian3Qt473\bin\qtenvS3.bat
```   

### Modifying bld.inf    

The sbsv2 does not understand PRJ\_PLATFORMS lists, so you’ll have to remove those. I left only PRJ\_MMPFILES definitions in the bld.inf files.  

### Building with sbsv2   
Here’s a list of couple of useful sbsv2 build command

```
sbs -c armv5_udeb_gcce                       - debug build with GCCE
sbs reallyclean                              - cleans everthing
sbs clean
```    

### Building with qmake   
To build with qmake from command line you’ll only need to run the qtenvs3.bat located at QtSDK\\Symbian\\SDKs\\Symbian3Qt473\\bin  
Here’s a list of couple useful build commands:

```
qmake -spec symbian-sbsv2                      - uses sbsv2
make debug-gcce                                - makes debug with GCCE
make distclean                                 - cleans everthing
```   

### Configuring the old abld-build to the QtSDK     
I don’t know why anyone would still like to use the old abld-build, but it still seems to be working with the new QtSDKs too. 

1. First add a new device for the QtSDK, and set it into default    

```
devices -add C:\QtSDK\Symbian\SDKs\Symbian3Qt473 C:\QtSDK\Symbian\SDKs\Symbian3Qt473
@Symbian3_Qt473:com.nokia.Symbian3_QtSDK473]
```   

2. Then set the new device as default    
```
devices -setdefault @Symbian3_Qt473:com.nokia.Symbian3_QtSDK473
```   

3. Set the new EPCOROOT    
```
set EPOCROOT=\QtSDK\Symbian\SDKs\Symbian3Qt473\
```    

4. build with able-build as you used to.

---
id: 502
title: 'MinGW Symbian Build Chain'
date: '2009-04-15T18:32:19+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=502'
permalink: /502/
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
aktt_tweeted:
    - '1'
categories:
    - 'MinGW buidchain'
    - 'Symbian Development'
tags:
    - ARM
    - assembler
    - gpsp
    - MinGW
    - msys
    - porting
---

I saw harry Li’s blog post about generic [symbian makefile,](http://blogs.forum.nokia.com/blog/harry-lis-forum-nokia-blog/2009/02/10/a-generic-makefile-build-script-for-symbian) and I found it very interesting. The makefile seems to be a very good tool for porting software from other platforms into Symbian OS.  
The MinGW in also nice build solution, since it doesn’t modifiy existing environment, so it can be used in parallel with old build setup. My version of the generic makefile is using newer GCCP and it supports assembly files and static libraries. This is a nice setup for building asm optimized sources in Symbian environment. If you also want to use newer version of GCCE you should see [forum.nokia wiki page](http://wiki.forum.nokia.com/index.php/How_to_use_GCCE_4_with_Symbian_SDKs) about the update process( changes in header files etc).  
The MinGW makes it easy to modify the build, so we have a better control of the build process than mystical Symbian OS buildchain. It took less than 10 minutes to add the support for assembler. It’s also very fast to change between two GCCE versions with this.  
I made some small modifications for my own purposes. Here are the instructions to use this environment.

1. install SVG2SVGConvertter. The installation file can be found under EPOCROOT\\S60tools\\svg2svgt\\installer\\
2. The script should be executed from \\gms directory. The script also expects to have \\dist\\gcce and \\obj\\gcce directories under the gms directory, so you should also make these folders.
3. The OS\_HRH part doesn’t seem to work in the defines.mk. I solved this my replacing the include statement in epoc32\\gcce\\gcce.h to ```
    #if defined(__PRODUCT_INCLUDE__)
     #include <variant/Symbian_OS.hrh> //for MinGW
     //#include __PRODUCT_INCLUDE__ //quick hack
     #endif
    ```

Some modifications for newer GCCE.

1. Modify the PATH variable and replace the old GCCE installation path with the new one.
2. Change also CC\_INSTALL\_PATH variable into new GCCE installation path
3. I modify the version numbers in scrips.

Know limitations:

1. There is no build for help files, and the svg conversion seems to be a bit limited. However the shouldn’t be any major issues, if old buildchain is still used for some builds.

Download the [makefile](/jekyll-export/wp-content/uploads/2009/04/makefile) and [defines.mk](/jekyll-export/wp-content/uploads/2009/04/defines.mk)  
a sample of config.mk is shown on below.

```
PROJECT_NAME = myproject
TARGET_TYPE = EXE
UID2 = 0
UID3 = DEADBABE
SECUREID = DEADBABE
EPOCSTACKSIZE = 80000
EPOCHEAPSIZE = 5000000 64000000
CAPABILITY = NONE
SYSINCLUDE = $(EPOCROOT2)/include $(EPOCROOT2)/include/esdl $(EPOCROOT2)/include/libc
USERINCLUDE = ../inc
CXXSRCS = \
 myapp.cpp \
 myApplication.cpp \
 myAppView.cpp \
 myAppUi.cpp \
 myDocument.cpp \
 $(NULL)
CSRCS = \
 main.c \
 $(NULL)
ASRCS = \
 my_asm_optimized_source.S \
 $(NULL)
RSS_TARGETS = $(DIST_PATH)/$(PROJECT_NAME).rsc $(DIST_PATH)/$(PROJECT_NAME)_reg.rsc
LANG_MACRO = SC
SYSLIBRARY = euser.lib avkon.lib eikcore.lib eiksrv.lib apparc.lib estlib.lib efsrv.lib cone.lib
STATICLIBRARY = mystaticlib.lib
CERT = /c/cert/gps60p.cert
KEY = /c/cert/gps60p.key
```

I tested the MinGW buildchain and scripts by compiling the gpSP (probably the best GBA emulator) from GP32 platform to Symbian OS. The gpSP was also nice test, since it uses the c preprocessor (cpp) alot, and the old Symbian buildchain fails miserably building the gpSP sources. However with MinGW the build looks very promising, so I’m really temptated to continue with this port.
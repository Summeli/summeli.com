---
id: 2247
title: 'Generic Makefile Build Chain for Symbian OS v. 1.1'
date: '2011-05-03T18:10:35+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2247'
permalink: /2247/
aktt_tweeted:
    - '1'
aktt_notify_twitter:
    - 'yes'
categories:
    - 'MinGW buidchain'
tags:
    - Debugging
    - MinGW
    - msys
    - porting
---

The build chain was originally made by [Harry Li](http://blogs.forum.nokia.com/blog/harry-lis-forum-nokia-blog/2009/02/10/a-generic-makefile-build-script-for-symbian). I just continued the project and added support for staticlibrary linking, debugging etc.  
**What’s new:**

- Support for QtCreator and Nokia QtSDK.
- GCCE was updated into 4.x in QtSDK, and that’s now being used in new build scripts.

**MOTIVATION**

- The C preprocessor can be used much better with makefile than with abld build. You can not compile a project relying heavily on c preprocessor with abld build, so the makefile build is really an essential tool for those projects.
- It makes porting software from linux based systems easier. The GCCE is just a GCC build for Symbian so now you can use GCC (hopefully almost same version) and same the build rules for the port in Symbian also.
- You can create static libs from the code that is hard to port (you need some custom compiling tricks), and then link into it from mmp-files or from Qt project files.
- The generic makefile build is also faster than the abld build. You could (hopefully) also make it faster with “-j” option with the future versions of GCCE

**INSTALLATION**  
Here are the instructions to use this environment.

1. Install [MSYS](http://www.mingw.org/wiki/msys)
2. The script should be executed from \\gms directory. The script also expects to have \\dist\\gcce and \\obj\\gcce directories under the gms directory, so you should also make these folders.
3. The OS\_HRH part doesn’t seem to work in the defines.mk. I solved this my replacing the include statement in epoc32\\gcce\\gcce.h to ```
    <pre class="brush: cpp; title: ; notranslate" title="">
    #if defined(__PRODUCT_INCLUDE__)
     #include <variant/Symbian_OS.hrh> //for MinGW
     //#include __PRODUCT_INCLUDE__ //quick hack
     #endif
    ```
    
    **![](http://www.summeli.com/wp-includes/js/tinymce/plugins/wordpress/img/trans.gif "More...")![](http://www.summeli.com/wp-includes/js/tinymce/plugins/wordpress/img/trans.gif "More...")**  
       
    **BUILDING WITH GENERAL MAKEFILE**  
    Build with this “Gnu Make for Symbian”, you need three files [Makefile](http://www.summeli.com/wp-content/uploads/2011/05/Makefile.txt), [defines.mk](http://www.summeli.com/wp-content/uploads/2009/09/defines.mk) and config.mk in ***myapp/gms*** path. You should also make folders ***myapp/gms/dist/gcce*** and ***myapp/gms/obj/gcce*** . Also three environment parameters should be set like this:
    
    
    - SYMBIAN\_SDK\_PATH = /c/QtSDK/Symbian/SDKs/Symbian3Qt473/
    - ACTIVE\_PERL = /c/QtSDK/Symbian/tools/perl/bin/perl.exe
    - CC\_INSTALL\_PATH = /c/QtSDK/Symbian/tools/gcce4/bin
    
    Please be noted the first one should contains a trailing slash like classic EPOCROOT environment variable. The second one is the ActivePerl .exe file used by some resource compiler script. The last one is the path to GCCE compiler installation path, without trailing slash. If there are spaces in any of them, please use **“\\ ”** backslash with a space instead.  
    After all these done, you could change your working directory into the build home by “***cd /c/myapp/gms***“. Then use the following commands to build.
    
    
    - “***make debug***” will do the debug build,
    - **“make release”** will do the release build
    - **“make clean”** will do the clean
    - “***make pack***” will also do the makesis work.
    
    a sample of config.mk is shown on below. The syntax is pretty similar to the mmp file. Note that if you are creating a static library, then you don’t have to define uid’s and libraries to be linked etc (as in mmp-files).
    
    ```
    <pre class="brush: cpp; title: ; notranslate" title="">
    PROJECT_NAME = myproject
    #valid target types are EXE, DLL and LIB(static lib)
    TARGET_TYPE = EXE
    UID2 = 0
    UID3 = 0xDEADBABE
    SECUREID = 0xDEADBABE
    EPOCSTACKSIZE = 80000
    EPOCHEAPSIZE = 5000000 64000000
    CAPABILITY = LocalServices+NetworkServices
    SYSINCLUDE = $(EPOCROOT2)/include $(EPOCROOT2)/include/platform $(EPOCROOT2)/include/libc
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
    CERT = /c/cert/mypro.cert
    KEY = /c/cert/mypro.key
    PASS =
    ```
    
    note that the capabilities are added with a “+” sign in between capabilties. The cert, key and pass variables are for app signing.  
    **DEBUGGING**  
    The QtCreator seems to be able to find the code without any help, so no special tricks required in here.  
    **KNOWN LIMITATIONS**
    
    
    1. There is no build for help files, and the svg conversion is a bit limited. However the shouldn’t be any major issues, since you can build these with standard abld symbian build chain.
    2. The WINSCW build is not support, nor it never will be. The tool is made primary for porting libraries from Linux to Symbian.
    
    **MODIFYING THE BUILD ENVIRONMENT**  
    Modifying the build environment is quite easy, if you have any previous experience of editing Makefiles. You should take a look at Symbian OS post-linker [“elf2e32” documentation](http://developer.symbian.com/main/documentation/sdl/symbian94/sdk/doc_source/ToolsAndUtilities94/Build-ref/Elf2E32Syntax.html) if you like to change any symbian OS specific values. For example EPOCALLOWDLL data will be “–dlldata” value to the post linker etc.  
    The GCCE documentation can be found from the Codesourcery’s site. Here is link to the [GCCE 4.x documentation](http://www.codesourcery.com/sgpp/lite/arm/portal/release1589)
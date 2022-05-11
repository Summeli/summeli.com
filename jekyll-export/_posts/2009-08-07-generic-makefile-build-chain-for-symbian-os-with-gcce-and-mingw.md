---
id: 1052
title: 'Generic Makefile Build Chain for Symbian OS With GCCE and MinGW'
date: '2009-08-07T17:21:09+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1052'
permalink: /1052/
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
    - Debugging
    - MinGW
    - msys
    - porting
---

The build chain was originally made by [Harry Li](http://blogs.forum.nokia.com/blog/harry-lis-forum-nokia-blog/2009/02/10/a-generic-makefile-build-script-for-symbian). I just continued the project and added support for static library linking, debugging etc.  
**MOTIVATION**

- The generic makefile gives you a better control of the build. You can define your own rules for each file, if you like. Therefore it’s also easier to fight against the compiler/build chain bugs.
- The C preprocessor can be used much better with makefile, than with abld build. You can not compile a project relying heavily on c preprocessor with abld build, so the makefile build makes the porting a lot easier.
- It makes porting software from linux based systems easier. The GCCE is just a GCC, build for Symbian so now you can use GCC (hopefully almost same version) and same the build rules for the project in Symbian also.
- The generic makefile build is also faster than the abld build.

**INSTALLATION**  
Here are the instructions to use this environment.

1. install SVG2SVGConvertter. The installation file can be found under EPOCROOT\\S60tools\\svg2svgt\\installer\\
2. The script should be executed from \\gms directory. The script also expects to have \\dist\\gcce and \\obj\\gcce directories under the gms directory, so you should also make these folders.
3. The OS\_HRH part doesn’t seem to work in the defines.mk. I solved this my replacing the include statement in epoc32\\gcce\\gcce.h to ```
    <pre class="brush: cpp; title: ; notranslate" title="">
    #if defined(__PRODUCT_INCLUDE__)
     #include <variant/Symbian_OS.hrh> //for MinGW
     //#include __PRODUCT_INCLUDE__ //quick hack
     #endif<br />
    ```
    
    ![](http://www.summeli.com/wp-includes/js/tinymce/plugins/wordpress/img/trans.gif "More...")

**BUILDING WITH GENERAL MAKEFILE**  
Build with this “Gnu Make for Symbian”, you need three files **[Makefile](http://www.summeli.com/wp-content/uploads/2009/08/Makefile)**, **[defines.mk](http://www.summeli.com/wp-content/uploads/2009/08/defines.mk)** and config.mk in ***myapp/gms*** path. You should also make folders ***myapp/gms/dist/gcce*** and ***myapp/gms/obj/gcce.***Then you need to install [MSYS](http://www.mingw.org/wiki/msys) . Also three environment parameters should be set like this:

- SYMBIAN\_SDK\_PATH = /c/symbian/9.1/s60\_3rd\_mr/
- ACTIVE\_PERL = /c/perl/bin/perl.exe
- CC\_INSTALL\_PATH = /c/Program\\Files/CSL\\ Code\\ Sourcery

Please be noted the first one should contains a trailing slash like classic EPOCROOT environment variable. The second one is the ActivePerl .exe file used by some resource compiler script. The last one is the path to GCCE compiler installation path, without trailing slash. If there are spaces in any of them, please use **“\\ ”** backslash with a space instead.  
After all these done, you could change your working directory into the build home by “***cd /c/myapp/gms***“. Then use the following commands to build.

- “***make debug***” will do the debug build,
- **“make release”** will do the release build
- **“make clean”** will do the clean
- “***make pack***” will also do the makesis work.

a sample of config.mk is shown on below.

```
<pre class="brush: cpp; title: ; notranslate" title="">
PROJECT_NAME = myproject
TARGET_TYPE = EXE
UID2 = 0
UID3 = 0xDEADBABE
SECUREID = 0xDEADBABE
EPOCSTACKSIZE = 80000
EPOCHEAPSIZE = 5000000 64000000
CAPABILITY = LocalServices+NetworkServices
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
PASS =
```

note that the capabilities are added with a “+” sign in between capabilties. The cert, key and pass variables are for app signing.  
**DEBUGGING**  
You have to be able to take the source files into your workspace in carbide, so you have to make a standard Symbian OS project from them. It does not have to compile, we just need to get the files into the workspace. Just make a standard bld.inf file and mmp-file where you list all the source files for the project.  
We are not going to build the project so we have to undo the building. Go to Window &gt; Preferences &gt; Run/Debug &gt; Launching and then untick “Build (if required) before launching”.  
![](http://www.summeli.com/wp-includes/js/tinymce/plugins/wordpress/img/trans.gif "More...")

<div class="wp-caption aligncenter" style="width: 310px">[![carbide_nobuild](http://www.summeli.com/wp-content/uploads/2009/07/carbide_nobuild-300x270.jpg "carbide_nobuild")](http://www.summeli.com/wp-content/uploads/2009/07/carbide_nobuild.jpeg)untick "Build (if required) before launching".

</div>  
Then just right click the project and select Debug as -&gt; Debug Configurations and configure the TRK and debugging stuff as you usually do. Then go into the Executables tab and select “Executables selected below” in “Load symbols for these executables and target them for debugging”. Now click add and find you executable under epoc32\\release\\gcce\\udeb folder and start debugging with TRK.  
**KNOWN LIMITATIONS** 1. There is no build for help files, and the svg conversion is a bit limited. However the shouldn’t be any major issues, since you can build these with standard abld symbian build chain.

**MODIFYING THE BUILD ENVIRONMENT**  
Modifying the build environment is quite easy, if you have any previous experience of editing Makefiles. You should take a look at Symbian OS post-linker [“elf2e32” documentation](http://developer.symbian.com/main/documentation/sdl/symbian94/sdk/doc_source/ToolsAndUtilities94/Build-ref/Elf2E32Syntax.html) if you like to change any symbian OS specific values. For example EPOCALLOWDLL data will be “–dlldata” value to the post linker etc.  
The GCCE documentation can be found from the Codesourcery’s site. Here is link to the [2009q1 release documentation. ](http://www.codesourcery.com/sgpp/lite/arm/portal/release822)  
**GCCE UPDATE**  
If you also want to use newer version of GCCE you should see [forum.nokia wiki page](http://wiki.forum.nokia.com/index.php/How_to_use_GCCE_4_with_Symbian_SDKs) about the update process( changes in header files etc). You should make following modification to the MinGW build chain for newer gcce.

1. Modify the PATH variable and replace the old GCCE installation path with the new one.
2. Change also CC\_INSTALL\_PATH variable into new GCCE installation path
3. I modify the version numbers in scrips.
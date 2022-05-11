---
id: 1274
title: 'Generic Makefile Build Chain for Symbian OS v. 1.0'
date: '2009-09-30T17:55:16+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1274'
permalink: /1274/
syntaxhighlighter_encoded:
    - '1'
aktt_notify_twitter:
    - 'yes'
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

The build chain was originally made by [Harry Li](http://blogs.forum.nokia.com/blog/harry-lis-forum-nokia-blog/2009/02/10/a-generic-makefile-build-script-for-symbian). I just continued the project and added support for static library linking, debugging etc. **The 1.0 version can also build static libs, which can easily be linked from Symbian .mmp files,or Qt’s .pro files.** Now we should be able to use the old already ported symbian engines(gpsp etc) with Qt too, so the porting process from the old Avkon based UI system to the Qt’s UI should be more pleasant 🙂  
**MOTIVATION**

- The C preprocessor can be used much better with makefile than with abld build. You can not compile a project relying heavily on c preprocessor with abld build, so the makefile build is really an essential tool for those projects.
- It makes porting software from linux based systems easier. The GCCE is just a GCC build for Symbian so now you can use GCC (hopefully almost same version) and same the build rules for the port in Symbian also.
- You can create static libs from the code that is hard to port (you need some custom compiling tricks), and then link into it from mmp-files or from Qt project files.
- The generic makefile build is also faster than the abld build. You could (hopefully) also make it faster with “-j” option with the future versions of GCCE

**INSTALLATION**  
Here are the instructions to use this environment.

1. install SVG2SVGConvertter. The installation file can be found under EPOCROOT\\S60tools\\svg2svgt\\installer\\
2. The script should be executed from \\gms directory. The script also expects to have \\dist\\gcce and \\obj\\gcce directories under the gms directory, so you should also make these folders.
3. The OS\_HRH part doesn’t seem to work in the defines.mk. I solved this my replacing the include statement in epoc32\\gcce\\gcce.h to ```
    <pre class="brush: cpp; title: ; notranslate" title="">
    #if defined(__PRODUCT_INCLUDE__)
     #include &amp;lt;variant/Symbian_OS.hrh&amp;gt; //for MinGW
     //#include __PRODUCT_INCLUDE__ //quick hack
     #endif
    
    <p><img alt="" src="http://www.summeli.com/wp-includes/js/tinymce/plugins/wordpress/img/trans.gif" title="More..."></img></p>
    ```

  
**BUILDING WITH GENERAL MAKEFILE**  
Build with this “Gnu Make for Symbian”, you need three files [Makefile](http://www.summeli.com/wp-content/uploads/2009/09/Makefile), [defines.mk](http://www.summeli.com/wp-content/uploads/2009/09/defines.mk) and config.mk in ***myapp/gms*** path. You should also make folders ***myapp/gms/dist/gcce*** and ***myapp/gms/obj/gcce.***Then you need to install [MSYS](http://www.mingw.org/wiki/msys) . Also three environment parameters should be set like this:

- SYMBIAN\_SDK\_PATH = /c/symbian/9.1/s60\_3rd\_mr/
- ACTIVE\_PERL = /c/perl/bin/perl.exe
- CC\_INSTALL\_PATH = /c/Program\\Files/CSL\\ Code\\ Sourcery

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
CERT = /c/cert/mypro.cert
KEY = /c/cert/mypro.key
PASS =

<p>note that the capabilities are added with a “+” sign in between capabilties. The cert, key and pass variables are for app signing.<br></br>
<strong>DEBUGGING</strong><br></br>
You have to be able to take the source files into your workspace in carbide, so you have to make a standard Symbian OS project from them. It does not have to compile, we just need to get the files into the workspace. Just make a standard bld.inf file and mmp-file where you list all the source files for the project.<br></br>
We are not going to build the project so we have to undo the building. Go to Window > Preferences > Run/Debug > Launching and then untick “Build (if required) before launching”.<br></br>
<img alt="" src="http://www.summeli.com/wp-includes/js/tinymce/plugins/wordpress/img/trans.gif" title="More..."></img></p>
<div class="mceIEcenter">
<dl class="aligncenter" style="width: 310px;">
<dt><img alt="" class="alignnone size-medium wp-image-1006" height="271" loading="lazy" sizes="(max-width: 300px) 100vw, 300px" src="/wp-content/uploads/2009/07/carbide_nobuild-300x271.jpeg" srcset="/wp-content/uploads/2009/07/carbide_nobuild-300x271.jpeg 300w, /wp-content/uploads/2009/07/carbide_nobuild.jpeg 640w" width="300"></img></dt>
<dd>untick “Build (if required) before launching”.</dd>
</dl>
</div>
<p>Then just right click the project and select Debug as -> Debug Configurations and configure the TRK and debugging stuff as you usually do. Then go into the Executables tab and select “Executables selected below” in “Load symbols for these executables and target them for debugging”. Now click add and find you executable under epoc32\release\gcce\udeb folder and start debugging with TRK.<br></br>
<strong>KNOWN LIMITATIONS<br></br>
</strong></p>
<ol>
<li>There is no build for help files, and the svg conversion is a bit limited. However the shouldn’t be any major issues, since you can build these with standard abld symbian build chain.</li>
<li>The WINSCW build is not support, nor it never will be. The tool is made primary for porting libraries from Linux to Symbian.</li>
</ol>
<p><strong>MODIFYING THE BUILD ENVIRONMENT</strong><br></br>
Modifying the build environment is quite easy, if you have any previous experience of editing Makefiles. You should take a look at Symbian OS post-linker <a href="http://developer.symbian.com/main/documentation/sdl/symbian94/sdk/doc_source/ToolsAndUtilities94/Build-ref/Elf2E32Syntax.html">“elf2e32” documentation</a> if you like to change any symbian OS specific values. For example EPOCALLOWDLL data will be  “–dlldata” value to the post linker etc.<br></br>
The GCCE documentation can be found from the Codesourcery’s site. Here is link to the <a href="http://www.codesourcery.com/sgpp/lite/arm/portal/release822">2009q1 release documentation. </a><br></br>
<strong>GCCE UPDATE</strong><br></br>
If you also want to use newer version of GCCE you should see <a href="http://wiki.forum.nokia.com/index.php/How_to_use_GCCE_4_with_Symbian_SDKs">forum.nokia wiki page</a> about the update process( changes in header files etc). You should make following modification to the MinGW build chain for newer GCCE.</p>
<ol>
<li>Modify the PATH variable and replace the old GCCE installation path with the new one.</li>
<li>Change also CC_INSTALL_PATH variable into new GCCE installation path</li>
</ol>
```
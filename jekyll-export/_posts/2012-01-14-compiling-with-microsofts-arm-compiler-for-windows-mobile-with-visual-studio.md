---
id: 2802
title: 'Compiling with Microsoft&#8217;s ARM compiler for Windows Mobile with Visual Studio'
date: '2012-01-14T15:40:16+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2802'
permalink: /2802/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Windows Phone Development'
tags:
    - 'native code'
    - 'visual studio'
    - 'windows mobile'
    - wp7
---

I have played with Visual Studio 2008 and Microsoft Mobile SDK to build some native code for windows phone. This is pretty much a LOG for myself, since I tend to forget things. Currently I have the Snes9x sources compiled inside a native COM DLL, which I can use from the managed wp7 code. Don’t get too excited since that code probably don’t work at all (yet), but it’s a nice start, and I like to learn how to use new tools by using them.  
I started by building the snes9x sources as a one static library, and including that library from a COM DLL, which will define the interface the to managed code. It’s a nice way to build an app, since I can easily separate the COM communication interface and the snes9x code.

#### The Environment

You can not actually build a native library with Windows Phone SDK, but it seems that you can build a COM DLL with Windows Mobile SDK, and use that from the managed code. This is totally unsupported “feature”, so everything might not work as you expect 😉  
First you must install Visual Studio 2008 and Windows Mobile SDK. You can get more details of the native environment from[ Heathcliff74 XDA-developers post](http://forum.xda-developers.com/showthread.php?t=1299134)  
I installed the good old Windows XP inside a virtual box, and then I installed

1. [Visual Studio 2008](http://www.microsoft.com/visualstudio/en-us/products/2008-editions) with [latest service pack](http://www.microsoft.com/download/en/details.aspx?id=10986) and hotfixes.
2. [Windows Mobile 6 Professional SDK Refresh](http://www.microsoft.com/download/en/details.aspx?id=6135).

<div>After everything has been installed we can start the development by creating a new static library.</div><div>#### Creating a static library

To create a static library you should create a new project (file/new project). Choose Visual c++ / Smart Device / **Win32 Smart Device Project**. Then choose Application settings, and choose application type, and use “static library”

</div>#### Precompiler settings

You can find the Precompiler settings in Visual studio under **project/settings/c/c++/Preprocessor tab**.

<div class="wp-caption aligncenter" id="attachment_2829" style="width: 310px">[![](http://www.summeli.com/wp-content/uploads/2012/01/vs_preprocessor-300x207.png "project/settings/c/c")](http://www.summeli.com/wp-content/uploads/2012/01/vs_preprocessor.png)project/settings/c/c

</div>#### Precompiled headers

I had not used the precompiled headers before, so this was a new feature for me. I recommend reading Wikipedia’s [Precompiled header](http://en.wikipedia.org/wiki/Precompiled_header) article for more details how it works etc. Precompiled header is basically a big header file compiled from multiple header files. It’s a nice idea, and it could reduce the build time, but sadly it seems to totally mess up my static lib project, so I decided to live without it.  
The precompiled header can be turned on/off under **project/settings/c/c++/Precompiled Headers**

#### Creating a COM DLL

To create a COM DLL you should create a new project (file/new project). Choose Visual c++ / Smart Device / **ALT Smart Device project**. Then choose Dynamic Link Library under application settings.

#### Including a static library

First you must add a reference into you project ( the COM project in my case). Right click the project, and choose “References..”. And the next dialog you can click “Add Reference” and add your new static library project as a reference.  
Next add the static library as a project dependency by right clicking the project and choose “project dependencies” and you can choose the new static libraries as dependencies to your project.

<div class="wp-caption aligncenter" id="attachment_2830" style="width: 310px">[![](http://www.summeli.com/wp-content/uploads/2012/01/references-300x205.png "project references")](http://www.summeli.com/wp-content/uploads/2012/01/references.png)project references

</div>#### Adding Include Dirs

You can add Include Dirs into the project under **project/settings/c/c++/General**

#### Building the COM DLL

After I have added the static libs, and the proper include directories (pointing at the static libs) I can successfully build the project. I decided to use the “precompiled headers” with my COM library, since it’s not breaking anything.

#### Next steps

I’ll probably start playing with the COM interface, and see what I can do with this code. It’s still quite possible that everything is totally broken, and I didn’t accomplish anything, but it was still nice to play with new tools etc.
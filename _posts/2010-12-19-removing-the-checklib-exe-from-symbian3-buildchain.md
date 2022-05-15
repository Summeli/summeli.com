---
id: 2171
title: 'Removing the checklib from Symbian^3 SBSv1 build chain'
date: '2010-12-19T23:19:03+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2171'
permalink: /2171/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - checklib
---

According to the Symbian documentation the checklib.exe is a static analysis tool for checking the consistent use of operator new in static libraries linked into dll or exe. This means that you should use the symbian way of operator new with (ELeave), or you should use the standard C++ way of operator new. In Qt apps you are in standard c++ world, and in Avkon apps you’re in Symbian c++ world.  

The idea of checklib is pretty good. You might run into some troubles with the inconsistent use of new operator in out of memory situations, and debugging these errors can be time consuming. So getting a warning about them feels like a nice feature from the SDK.     

The problem is that the checklib errors will fail your whole build, if an inconsistency is found (it’s not just a warning).Failing the build doesn’t really make any sense, since it’s a static code analysis tool. I think that I would like the checklib, if it would only give me a warning like “the way you’re using operator new is not consistent, see forum.nokia.com for more info”  

But unfortunately the checklib will just fail the whole build. The worst part is that the tool itself doesn’t give you any hints what symbol to look at (where the problem is).  
Here are some common error codes from checklib:

```
checklib error: "foo is incompatible with standard C++"
checklib: error: not a COFF object: bad magic.
checklib: error: file can not be found.
```    

These errors just don’t help me even a bit, and I really don’t care that much about the OOM situations. I’m using a lot of my own memory hacks anyway, so I’m pretty much screwed in OOM anyway.  
Here’s how you can remove this stupid tool from the SBSv1 build chain   
  
Open files cl\_bpabi.pm and cl\_codewarrior.pm under \\epoc32\\tools  
and modify the lines with:    

```
$run_checklib = 1;
```

into:   

```
<pre class="brush: plain; title: ; notranslate" title="">
$run_checklib = 0;
```

If you already have a project in carbide, and you just found this page by googling the checklib related problems remember also to do the regular

```
abld really clean
bld clean
```   

Double check also that you don’t have anything related to to your project under \\epoc32\\build directory. If you can find a directory with your project name on it, delete it. You should get a working makefile under the build directory after recreating the project.
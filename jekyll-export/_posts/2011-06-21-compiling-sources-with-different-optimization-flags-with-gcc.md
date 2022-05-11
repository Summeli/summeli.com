---
id: 2551
title: 'Compiling sources with different optimization flags with GCC'
date: '2011-06-21T22:44:52+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2551'
permalink: /2551/
aktt_tweeted:
    - '1'
aktt_notify_twitter:
    - 'yes'
categories:
    - ARM
    - 'Symbian Development'
---

I had some strange problems with some GCC bugs with AntSnes and gpsp. For some reason some source files did not compile correctly with “-O2” optimization flags. A quick way to fix this problem was to compile the objects with problems without optimizations.  
My quick “hacky” solution was to compile these few files with “-O0” flags into the asm-files from command line, and then include these asm-files from the mmp/makefile into the project.  
Compiling the sources into asm-listings can be done like this:

```
<pre class="brush: plain; title: ; notranslate" title="">
 gcc -O0 -S -c foo.c
```

Of course you’ll get some problems from missing included etc, but that can be solved by adding all the include folders to the gcc with “-include” flag.
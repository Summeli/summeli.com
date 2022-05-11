---
id: 107
title: 'Compiling assembly sources in S60 project'
date: '2008-12-31T18:00:51+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=107'
permalink: /107/
aktt_notify_twitter:
    - 'no'
categories:
    - 'Symbian Development'
tags:
    - ARM
    - assembler
    - porting
---

Compiling assembly sources with different build options is not easy with Symbian OS MMP-files. You can add assembly files as normal sources, but then they will be compiled with same rules as all other files in the project, which can cause problems. My solution was to make a separate build for assembly sources.  
I’m building the assembly sources from command line. You can use the GCCE’s assembler arm-none-symbianelf-as.exe directly. Building asm\_func.s source for an example:

```
<pre class="brush: cpp; title: ; notranslate" title="">
arm-none-symbianelf-as.exe asm_func.s -marmv4t -mthumb-interwork -o asm_func.o
```

Now we have an object file asm\_func.o. Copy the object file to \\epoc32\\release\\armv5\\urel. Now the object file can be added to the project as a static library. Just put the following line into your mmp-file:

```
<pre class="brush: cpp; title: ; notranslate" title="">
STATICLIBRARY	asm_func.o
```

Adding object files as a static library seems like a strange idea at start, but it actually makes sense. After all a static library is just a collection of object files, so why not use a single object file.
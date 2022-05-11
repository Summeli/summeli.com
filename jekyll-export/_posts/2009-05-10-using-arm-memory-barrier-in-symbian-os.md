---
id: 632
title: 'Using ARM Memory Barrier in Symbian OS'
date: '2009-05-10T00:26:02+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=632'
permalink: /632/
aktt_tweeted:
    - '1'
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
categories:
    - ARM
    - 'Symbian Development'
tags:
    - ARM
    - gpsp
---

Today I have been digging the methods to to make a [gpSP( I think this is the best GBA emulator)](http://wiki.gp2x.org/wiki/GpSP) port to Symbian OS.Thanks to the Exophase for developing this wonderful piece of software and for ZodTTD for the awesome ARM port! The gpSP is running “generated” ARM binary in the ARM processor’s memory, so the Memory Barrier has to be used. The next problem is to get the code running on the ARM under Symbian OS.  
The [ARM9 reference manual](http://www.atmel.com/dyn/resources/prod_documents/arm_926ejs_trm.pdf) tells this about Memory Barrier.

> Whenever code is treated as data, for example self-modifying code, or loading code into  
> memory, then a sequence of instructions called an Instruction Memory Barrier (IMB)  
> operation must be used to ensure consistency between the data and instruction streams  
> processed by the ARM926EJ-S processor.  
> Usually the instruction and data streams are considered to be completely independent  
> by the ARM926EJ-S processor memory system, and any changes in the data side are  
> not automatically reflected in the instruction side. For example if code is modified in  
> main memory then the ICache might contain stale entries. To remove these stale entries  
> part or all of the ICache must be invalidated.

In Symbian OS the Kernel should take care about ICache invalidation. The Symbian has User library for user side interaction with the Kernel. If we want to generate our own code and run it in specific memory are, we have to first tell to the kernel to threat this area as code. The code example for doing this is below.

```
<pre class="brush: cpp; title: ; notranslate" title="">
RChunk codechunk;
TInt error = codechunk.CreateLocalCode(codechunk_size,codechunk_siz);
void* codechunk_ptr = codechunk.Base();
```

Now the codechunk is created. The ARM documentation told that ICache must be invalidated before executing the code. The Symbian should take care for invalidating the ICache, when IMB\_Range is called.

```
<pre class="brush: cpp; title: ; notranslate" title="">
void CLEAR_INSN_CACHE(void* code, int size)
{
User::IMB_Range( code, (void*)(code + size));
}
```
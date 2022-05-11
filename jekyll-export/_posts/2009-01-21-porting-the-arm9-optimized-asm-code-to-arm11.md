---
id: 218
title: 'Porting the ARM9 optimized asm code to ARM11'
date: '2009-01-21T00:02:12+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=218'
permalink: /218/
aktt_notify_twitter:
    - 'no'
categories:
    - ARM
    - 'Symbian Development'
tags:
    - ARM
    - assembler
---

This is just a short post about my modifications to the Snes9x assembly sources. You can find the sources at the 0.1[ release post.](http://www.summeli.com/?p=166) Actually there was only one modification required, which I will share with you. It might help others to port fast assembly code to ARM11 processors.  
ARM9 optimized source:

```
<pre class="brush: cpp; title: ; notranslate" title="">
STMFD    R13!,{PC} @ Push return address
MOV    R1,#0
B    myASMFunc
B   arm9ReturnPoint
```

and the function return in myASMFuc with code

```
<pre class="brush: cpp; title: ; notranslate" title="">
LDMFD        R13!,{PC}
```

The function will return to the ARM9Return point in ARM9 processor. However with ARM11 processor it will access again to the myASMFunc. <span style="text-decoration: line-through;">The ARM9 seems to have some latency accessing to the stack, which ARM11 doesn’t have. a cleaver ARM9 programmer has made nice optimization, which has to be removed from ARM11 support.</span> The ARM9 processor has different str/stm instuctions than the ARM11 in OMAP processor.  
Thanks for notas comment:  
“Such instructions \[str/stm\] can store either the address of the instruction plus 8 bytes, like other instructions that read R15, or the address of the instruction plus 12 bytes. Whether the offset of 8 or the offset of 12 is used is IMPLEMENTATION DEFINED.”  
Therefore we have to fix it to the ARM11 version, which should look like this:

```
<pre class="brush: cpp; title: ; notranslate" title="">
MOV    R1,#0 @deoptimize for ARM11 support
STMFD    R13!,{PC} @ Push return address
B    myASMFunc
B   arm11ReturnPoint @ARM11 gets here when instructions are reordered
```

Usually the assembly code could be even more optimized for ARM11 than ARM9, since ARM11 has more signal processing related instructions. However I don’t think that those instructions give much help for emulating Snes. Maybe for some other emulators, and it definitely in signal processing tasks, like in developing codecs.  
**S60/Symbian/GCCE related issues:**  
It was really hard to get the stack properly aligned with GCCE and symbian. The solution was to give gcce a zero optimization flag -O0 and then manually give all optimization flags. I know. It looks stupid, but it worked…

```
<pre class="brush: cpp; title: ; notranslate" title="">
OPTION GCCE -march=armv5t -O0 -fexpensive-optimizations -finline -finline-function -ffast-math -msoft-float -falign-functions=32 -falign-loops -falign-labels -falign-jumps -fomit-frame-pointer
```

One ohter strange thing is binary size. With S60 FP1 the binary size is about 1200kB and with S60 3.0 MR release I will get about 300kB. Both with same functionality. Perhaps the FP1 add the debug symbols in each binary, even when they are not required.
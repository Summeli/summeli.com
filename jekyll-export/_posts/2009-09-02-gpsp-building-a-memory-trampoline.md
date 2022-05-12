---
id: 1106
title: 'gpSP: Building A Memory Trampoline'
date: '2009-09-02T16:40:53+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1106'
permalink: /1106/
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
aktt_tweeted:
    - '1'
categories:
    - ARM
    - 'Symbian Development'
tags:
    - ARM
    - assembler
    - gpsp
    - N95
    - porting
    - psx4symbian
---

Thanks to the original gpSP creator Exophase for tips. I was really confused with BL instructions and the fact that the memory address was pointing into wrong memory area. The problem was in Symbian OS memory mappings. It’s a very common problem with dynarec and Symbian. I had pr  
In Symbian you can create memory partitions for dynamic recompilation with CreateLocalCode and IMB\_Range deal, as [I wrote few moths ago](/632). The problem is the way how Symbian OS maps the memory. The pointer to the dynamic code area is too far from the ‘static code’. The BL instruction has a limit of +-32MB. The memory memory is mapped in different way, so we can not use the BL instruction to get to the static code from the dynamic code.  
BLX instruction would have longer range than BL, so that could be used. Using the BLX instruction would look like this.

```
ldr reg, =address
blx reg
```

The ldr instruction is actually meta-code and compiles into something like this:

```
mov reg,#0xYYY
orr reg,reg,#0xYY000
orr reg,reg,#0xYY00000
orr reg,reg,#0xY0000000
bx reg
```

However the way the calling code skips over the bl instruction by adding a shifted bit to the pc it is impossible to replace this call with the register load plus BLX instruction. The solution is to make stubs to the ‘dynamic’ memory area for each function call instead, and then call the stub with bl, and use bx from that stub to reach out to the final destination.  
  
example stub:

```
ldr reg, =address
bx reg
```

generating calls to the stub from dynamic memory area:

```
bl #relative_offset_to_the_stub
```

So after branch from the actual code, we end up to the stub, and from there the code branches to the actual function. This is actually a big de-optimization to the gpsp, but it’s the only way to get it working. The memory trampoline could also be described with an image below.

[![memory trampoline](/jekyll-export/wp-content/uploads/2009/08/memory_trampoline.jpg)](/jekyll-export/wp-content/uploads/2009/08/memory_trampoline.jpg)   

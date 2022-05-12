---
id: 555
title: 'Degugging gpSP'
date: '2009-08-04T18:49:36+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=555'
permalink: /555/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - gpsp
    - S60
---

The porting process of gpSP has been going forward quite well until this came up. The code behavior in debug session seems to be very strange.  
The following code should branch into the address located in register r0. The address 0x9cc00080 is marked as code in Symbian OS, and IMB\_Range() has been called in prior to execution.

```
bx r0  @r0 value is 0x9cc00080
```

However, when debugging it seems that the pc is going into address 0x9b14a4a8.  
Here is some debug data from carbide:

1. call stack
2. registers during this time
3. memory starting from 0x9cc00078. It seem to be mapped to code
4. call stack after branch
5. registers after branch

 

 [![](/jekyll-export/wp-content/uploads/2009/05/debug2_registers-150x150.jpg)](/jekyll-export/wp-content/uploads/2009/05/debug2_registers.jpg) | [![](/jekyll-export/wp-content/uploads/2009/05/debug2_stack-150x150.jpg)](/jekyll-export/wp-content/uploads/2009/05/debug2_stack.jpg) | [![](/jekyll-export/wp-content/uploads/2009/05/debug_memory-150x150.jpg)](/jekyll-export/wp-content/uploads/2009/05/debug_memory.jpg) 


[![](/jekyll-export/wp-content/uploads/2009/05/debug_registers-150x150.jpg)](/jekyll-export/wp-content/uploads/2009/05/debug_registers.jpg) | [![](/jekyll-export/wp-content/uploads/2009/05/debug_stack-150x150.jpg)](/jekyll-export/wp-content/uploads/2009/05/debug_stack.jpg) | [![](/jekyll-export/wp-content/uploads/2009/08/generated_memory-150x150.jpg)](/jekyll-export/wp-content/uploads/2009/08/generated_memory.jpg)

I really can’t tell why this is behaving in such odd way. Hopefully some ARM guru is reading this and knows the cause for this problem.  
I’ll make a post, when i’ll get this one solved…  
  
### Update  
I copyed the memory from the memory area that should be executed. I’m hoping to find some guys from gp32x to see, if they have similar memory in execute\_arm\_translate function before the first branch. If the memory seems different, then that would explain a lot.. here is the memory in a text. file[ memory.txt](/jekyll-export//wp-content/uploads/2009/08/memory.txt)  
I originally used N96 with ARM9. I wanted to test this code also with N95 and a newer ARM11 processor. The debugger worked a lot better with N95. Here is the \_real\_ crash.  
[![generated_memory](/jekyll-export/wp-content/uploads/2009/08/generated_memory.jpg "generated_memory")](/jekyll-export/wp-content/uploads/2009/08/generated_memory.jpg)   
generated memory in N95

This one shows that it jumps correctly into the generated code area and it even works. However branch avay from the generated code is the problem. After this it will be in the unknown opcode. This is the point where the N96 actually crashes, the debugger just can’t handle the generated code are correctly.  
The lesson is to use N95 for debugging instead of crappy N96. However N96 was a great help in AntSnes porting, it helped me to point out the code that was working with ARM9 and failed with ARM11 and N95.  
The code is being executed inside the rom\_translation\_cache and it branches into the ram\_translation\_cache memory area. However that memory area is still null. Well, it gets easier now, since I now where to look at.. Hopefully I will be running the emulator on my next post 😉  

### Update 2:
The problem with the real crash was that the branch address weren’t inside the 32Mb limit of ARM processor. The solution was to implement [a memory trampoline](/1106) between the static and dynamic code blocks. 
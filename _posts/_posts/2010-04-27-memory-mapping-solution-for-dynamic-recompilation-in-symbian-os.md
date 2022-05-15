---
id: 1384
title: 'Memory Mapping solution for Dynamic Recompilation in Symbian OS'
date: '2010-04-27T19:57:45+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1384'
permalink: /1384/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - ARM
    - 'Symbian Development'
tags:
    - ARM
    - dynarec
    - gpsp
    - porting
---

The gpsp was my first emulator port with dynamic recompilation. The problem in memory mapping and dynarec is that local data in Symbian OS is too far away from the user area, where we the new memory chunk for the dynamic area was created. My first solution was the [memory trampoline](/1106) pattern.  
However I got an optimal solution from Olli Hinkka. The solution is called dynamic text segment relocation routine. Basically the relocator is relocating the process into the user memory are in Symbian. With this approach no memory trampoline is required, since the static side is close enough to the dynamic side.  
How to use it:  
You’ll need Olli Hinkka’s relocator code. You can find it at least from gpsp github.[ relocutils.h](http://github.com/Summeli/gpSP4Symbian/blob/master/inc/relocutils.h)[ relocator.cpp](http://github.com/Summeli/gpSP4Symbian/blob/master/src/relocator.cpp) and [relocator\_glue.S](http://github.com/Summeli/gpSP4Symbian/blob/master/src/relocator_glue.s)  
First you’ll have to relocate your process on the user area in the Symbian. The user local data area is between 0x04000000-0x38000000, see the[ Symbian OS memory map](http://developer.symbian.org/wiki/index.php/Symbian_OS_Internals/7._Memory_Models#Memory_map_2).I’m using 0x10000000 in this example.

```
#include "relocutils.h"
int main(int argc, char** argv)
{
  BEGIN_RELOCATED_CODE(0x10000000);
  // all code from the code section of this process is run in the specified address
  END_RELOCATED_CODE();
  // return to the original code section
}
```

The next step is to create a new memory chunk for the dynamic recompiler and move it close to the newly relocated code. The new code chunk has to be in 32Mb range from our process memory area.

```
void createDynamicMemoryArea()
{
  TInt error = process.GetMemoryInfo( info );
  if( error )
    return error;
  TUint32 programAddr = 0x10000000;//(TUint32) info.iCodeBase;
  programAddr += info.iCodeSize;
  //the distance must be less than 32Mb
  TUint32 destAddr = programAddr - KDistanceFromCodeSection;
  g_code_chunk = new RChunk();
  TInt err = CreateChunkAt(destAddr,minsize, maxsize );
}
//Creates a chunk into addr
TInt CreateChunkAt(TUint32 addr,TInt minsize, TInt maxsize )
{
  TInt err = g_code_chunk->CreateLocalCode( minsize, maxsize );
  if( err )
    return err;
  if ((TUint32)g_code_chunk->Base() != addr)
      {
      TUint offset = (TInt)g_code_chunk->Base();
      offset = addr-offset;
      g_code_chunk->Close();
      RChunk temp;
      if( offset > 0x7FFFFFFF )
     {
     //shit, offset too big :(
     return KErrNoMemory;
     }
      TInt chunkoffset = (TInt) offset;
      err = temp.CreateLocal(0,chunkoffset);
      if( err )
     {
     temp.Close();
     return err;
     }
      err = g_code_chunk->CreateLocalCode(minsize,maxsize);
      temp.Close();
      }
  return err;
}
```

We have now transferred our process into new memory area, which means that our code section runs in different memory address now. However the code relocation didn’t affect to the data section at all. Therefore we must update all function pointers used from the dynamic side of the code.

```
TUint addr = &my_old_funck;
ddr+=relocated_code_offset;
generatejump(addr); generate immediate b/bl
```
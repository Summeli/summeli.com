---
id: 755
title: 'Symbian Debuggin: memory &#038; register fump from exception'
date: '2009-07-28T19:39:47+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=755'
permalink: /755/
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - 'exception handler'
---

I made my own Exception handler to make the memory dump into a file. The memory dumps can be used for debugging purposes.  
See what to do with the memory dump from [NewLC article aobut tracking down the Hardware exceptions](http://www.newlc.com/fr/tracking-down-hardware-exceptions-hardware).

```
_LIT(KTestFile, "C:\\Data\\myExcepption.txt");
_LIT( KStackInfo, "StackInfo: ");
void ExceptionHandler(TExcType)
{
    RFs fs;
    RFile file;
    fs.Connect();
    file.Open(fs,KTestFile,EFileWrite);
    RDebug::Print(_L("Exception handler"));
    HBufC8* buf = HBufC8::NewLC(1000);
    TPtr8 ptr = buf->Des();
    RThread().Context(ptr);
    file.Write(ptr);
    //save register info into a file
    RDebug::Printf( "%S", buf );
    CleanupStack::PopAndDestroy();
}
```

  
Using the Exception handler. The Exception handler can be easily set by calling  
SetExceptionHandler function.

```
User::SetExceptionHandler(&ExceptionHandler,0xffffffff);
```

**Note that you can not use this at the same time with Carbide On device debugging**, since the TRK will use the same mechanism to catch exceptions from the Hardware.
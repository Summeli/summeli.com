---
id: 1475
title: 'Implementing AntSnes with Qt part 3: Running the emulation in worker thread'
date: '2010-01-26T20:16:43+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1475'
permalink: /1475/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Qt Development'
    - 'Symbian Development'
tags:
    - AntSnesQtDev
    - 'Qt Development'
    - Symbian
---

I decided to build a two threaded application. The main thread is for the UI, and the worker thread if for the emulator. This makes all porting easier in general, since now we can have a UI thread to handle all rendering, key I/O etc, and run the emulator thread as worker thread, which can emit the new processed frames to the UI thread etc.  
The Qt makes the threading extra easy:  
In my application I just inherited the emulator controller class from QThread, then I just call start() to start the thread. The QThread will guarantee that all slots will be executed in the context of that QThread after start has been called.  
Another nice trick is to use Qt::BlockingQueuedConnection as connection type when the signal must be prosessed before the emitting thread can continue.  
I’m really excited that all this communication between threads was so easy. No mutexes, or semaphores were required this time at all 🙂  
Here’s some code snippets how the threading was actually implemented.

```
<pre class="brush: cpp; title: ; notranslate" title="">
//starting the thread
void QSnesController::Start()
{
   start( QThread::LowPriority );
}
//after the start() the thread will execute in the run()
void QSnesController::run()
 {
 connect(this, SIGNAL(frameblit()), blitter, SLOT(render()),
 Qt::BlockingQueuedConnection );
 gameloop();
 disconnect(this, SIGNAL(frameblit()), blitter, SLOT(render()) );
 }
//in render frame callback function
emit( frameblit() );
```
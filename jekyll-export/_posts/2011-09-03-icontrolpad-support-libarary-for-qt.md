---
id: 2710
title: 'iControlPad support libarary for Qt'
date: '2011-09-03T11:44:47+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2710'
permalink: /2710/
aktt_tweeted:
    - '1'
aktt_notify_twitter:
    - 'yes'
categories:
    - 'Qt Development'
tags:
    - iControlPad
    - meego
    - Symbian
---

The iControlPad didn’t work in keyboard mode with Symbian devices, so I decided to make my own support library for it. The iControlPad is working on SPP mode as default, and that mode support also the analog nubs, so I decided to write support for it.  
You can get the support library from GitHub: <https://github.com/Summeli/iCP4Qt>  
**Integrating the library to your project**  
You only need to include the iCP4Qt pri file inside your project file

```
<pre class="brush: cpp; title: ; notranslate" title="">
include (iCP4Qt.pri)
```

**Connecting to the iControlPad**  
Connecting to the iControlPad is easy. Crete the iControlpad client, and then call connect:

```
<pre class="brush: cpp; title: ; notranslate" title="">
client = new iControlPadClient(this); //the keyEvents will be delivered to the parent
client->discoverAndConnect( iControlPadClient::iCPReadDigital );
```

Once connected, whe library will emit singal:

```
<pre class="brush: cpp; title: ; notranslate" title="">
void connectedToiControlPad();
```

And if the iControlPad was not found, then it’ll emit

```
<pre class="brush: cpp; title: ; notranslate" title="">
void iControlPadNotFound();
```

  
**Receiving keypress events**  
The key events are delivered via Qt’s standard event handler, so you can receive keyevents by implementing the keyevents in you object

```
<pre class="brush: cpp; title: ; notranslate" title="">
void keyPressEvent( QKeyEvent * event);
void keyReleaseEvent(QKeyEvent* event);
```

The analog nubs are delivered via analogNubsUpdated event

```
<pre class="brush: cpp; title: ; notranslate" title="">
void analogNubsUpdated( qint8 l_x,  qint8  l_y, qint8  r_x, qint8 r_y );
```

where l\_x and l\_r are the left nub coordinates and r\_x and r\_y are the right nub coordinates. Where +32 is full down or full right, and -32 is full up or full left. 0,0 is center.  
**Meego support**  
I’m developing this with N950 and it seems to be working pretty well.  
**Symbian Support**  
I’m having some trouble with the Symbian support. I’m building with SymbianSR1Qt474 and with QtMobility 1.2, which is “not yet mature enough for ovi store”, so it probably has some issues on it. Everything is build on top of QtMobility APIs so the Symbian should also be supported when the QtMobility 1.2 is officially distributed to the Symbian devices.
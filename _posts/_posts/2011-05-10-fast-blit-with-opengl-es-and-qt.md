---
id: 2324
title: 'Fast blit with OpenGl ES and Qt'
date: '2011-05-10T22:02:23+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2324'
permalink: /2324/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Qt Development'
tags:
    - 'OpenGL ES'
    - Qt4
    - scaling
---

In my previous post I wrote about blit with opengl es 2.0 texture upload. However I noticed that using just Qt’s QGLWidget and implementing only the paintEvent is as fast as the texture upload with pure OpenGL ES API.  
I guess that QGLWidget is making the drawing via OpenGL, since the performance seems to be equal to the texture blitting with the standard OpenGL ES API and texture uploading.  
The whole blit is taking less than 6ms, so it’s good enough for my emulator ports. The memcopy could probably be optimized away from the blit, but that’s not the bottleneck at least in the current AntSnes implementation.  
Here’s an example from the AntSnes how to blit with QGLWidget and paintevent.

```
void AntSnesQt::blit(int width, int height)
{
    if (buf != NULL)
    {
        delete buf;
        buf = NULL;
    }
    //memcopy into the new buffer, which will be blit to to screen in the paintEvent.
    buf = new QImage(GFX.Screen, width, height, GFX.RealPitch,
            QImage::Format_RGB16);
    //calling the repaint will cause a new paintEvent into the widget
    repaint();
}
void AntSnesQt::paintEvent(QPaintEvent *)
{
    QPainter painter;
    painter.begin(this);
    if (buf != NULL)
    {
        QRect target(96, 0, 448, 360);
        QRect source(0, 0, buf->width(), buf->height());
        painter.drawImage(target, *buf, source);
     }
     painter.end
}
```
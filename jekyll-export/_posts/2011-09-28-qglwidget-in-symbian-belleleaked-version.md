---
id: 2741
title: 'QGLWidget in Symbian Belle(leaked version)'
date: '2011-09-28T17:20:30+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2741'
permalink: /2741/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
---

Warning: This post is made only with leaked Symbian Belle. The official Nokia release might not have the problem described in this post.  
Here’s the problem: I implemented the blit in QGLWidget’s paintEvent(QPaintEvent \*) method. The idea was that the Qt would be using OpenGL ES for the blit, when I’m using the QGLWidget.  
Currently I’m only using the QPainter for the actual blit. Like this:

```
QPainter painter;
painter.begin(this);
//.... do the painting
painter.end();
```

However the method above seems to be failing in the Symbian Belle (only a black screen is shown), so the QGLWidget is clearly not working as well as it was in the Symbian Anna.  
Solution: I just converted the QGLWidget into a normal QWidget, and everything seems to be working. At least with the leaked Symbian Belle I can not see any significant difference in the fps compared to what it was with Symbian Anna and QGLWidget, so I’ll just leave it like this.  
I don’t know if the official Belle release will contain this bug or not. If the bug still exists, then I can make an error report to the Qt’s JIRA.
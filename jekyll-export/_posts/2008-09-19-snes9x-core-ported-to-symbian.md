---
id: 13482
title: 'Snes9x core ported to symbian'
date: '2008-09-19T19:25:13+03:00'
author: Summeli
layout: post
guid: 'http://koti.kapsi.fi/~summeli/blog/?p=4'
permalink: /13482/
aktt_notify_twitter:
    - 'yes'
categories:
    - 'Symbian Development'
tags:
    - porting
---

[![supermario world](http://www.summeli.com/wp-content/uploads/2008/09/mario.jpg "mario")](http://www.summeli.com/wp-content/uploads/2008/09/mario.jpg)

I managed to port the Snes9x c-core into Symbian. It was a lot easier than fighting with the ASM-core. The image is not blitted into whole screen as you can see and it’s really slow. It’s slow because the CDirectScreen access in Symbian doesn’t allow user to write directly into the screen buffer. So currently frame is written into Snes9x frame buffer, then copied into CFbsBitmap and then written into the screen with DSA. It’s really slow…about 2 FPS.

My next step will be OpenGL ES based rendering. I will put the frame as texture into the opengl pipeline and then render it to a surface. I hope that I will get decent FPS with this method.
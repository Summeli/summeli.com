---
id: 1568
title: 'Implementing AntSnes with Qt part 6: Final touch, using stylesheets'
date: '2010-04-14T19:35:11+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1568'
permalink: /1568/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Qt Development'
    - 'Symbian Development'
tags:
    - AntSnesQtDev
    - Symbian
---

The Qt’s default style tries to look as much your original S60 theme as possible. The big problem is that each phone can have very different theme, and then your application might look really bad.  
The good news is that you can write your own style, and use it in your own application.  
Here’s a “before image” with my Symbian foundation default theme and AntSnes:

<div class="mceTemp">![AntSnes with Symbian default theme](/wp-content/uploads/2010/04/antsnes_default_theme-300x169.jpg)

The default theme has a lot of problems. For example the default blue color is used, when Qt doesn’t know what color to use. The donw arrow is also way too big in the default Qt theme.

</div>![](/wp-content/uploads/2010/04/antsnes_with_style-300x169.jpg)

AntSnes with style sheet

The Style sheet makes a huge difference in here. Now I can add some nice application logo’s etc, and I know that the color fits the application style. For example using that black and green AntSnes text wouldn’t really work with my default theme 😉

The Qt style sheets syntax is really close to css. It’s really easy for anyone to modify these. Here’s couple of really good links for creating new style sheets with Qt:

1. [Qt 4.6.2 Stylesheet](http://doc.trolltech.com/4.6/stylesheet.html)
2. [Qt 4.6.2 Styleseet Examples](http://doc.trolltech.com/4.6/stylesheet-examples.html)

Creating the style sheets is also very easy, since the Qt Editor will update all of your controls immediately after you have modified the style sheet. The application looks a bit different on actual Symbian phone, but it’s close enough to do the editing with the Qt Editor only.  
I could make different style sheet for different environments. For example I could have different styles for Maemo and for Symbian. Here’s a short code clip how to load and set a style sheet to application.

```
<pre class="brush: cpp; title: ; notranslate" title="">
  QFile file(":/style/summelistyle.qss");
    if(!file.open(QFile::ReadOnly))
        {
         __DEBUG1("Unable to open file");
        }
    QString styleSheet = QLatin1String(file.readAll());
    qApp-&amp;amp;amp;gt;setStyleSheet(styleSheet);

<p>The AntSnes is now pretty close to complete. I hope that I can post a youtube video soon, and also to make the first release.</p>
```
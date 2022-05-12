---
id: 2669
title: 'Disabling Swipe from a Fullscreen Game'
date: '2011-07-19T17:03:28+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2669'
permalink: /2669/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Meego Development'
tags:
    - meego
    - swipe
---

The swipe is really annoying feature in fullscreen gaming (antsnes for example). Instead of controlling the game you might end up swiping the game into the background, which is not cool. Luckily the swipe can be disabled quite easily from QWidget based classes.  

Here’s how you can disable the swipe:

```
void disableSwipe()
{
    QWidget * activeWindow = QApplication::activeWindow();
    Display *dpy = QX11Info::display();
    Atom atom;
    unsigned int customRegion[4];
    customRegion[0] = 0;
    customRegion[1] = 0;
    customRegion[2] = 854;
    customRegion[3] = 480;
    atom = XInternAtom(dpy, "_MEEGOTOUCH_CUSTOM_REGION", False);
    XChangeProperty(dpy, activeWindow->effectiveWinId(),
            atom, XA_CARDINAL, 32, PropModeReplace,
            reinterpret_cast<unsigned char *>(&customRegion[0]), 4);
}
```

And here’s an example of enabling it:

```
void enableSwipe()
{
    QWidget * activeWindow = QApplication::activeWindow();
    Display *dpy = QX11Info::display();
    Atom atom;
    atom = XInternAtom(dpy, "_MEEGOTOUCH_CUSTOM_REGION", False);
    if(XDeleteProperty(dpy, activeWindow->effectiveWinId(), atom) < 0){
      qWarning("XDeleteProperty for _MEEGOTOUCH_CUSTOM_REGION returns <0");
      }
}
```
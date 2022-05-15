---
id: 557
title: 'QT Mobile UI design'
date: '2009-05-07T15:34:34+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=557'
permalink: /557/
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
aktt_tweeted:
    - '1'
categories:
    - 'Qt Development'
tags:
    - Qt4
    - S60
---

I have been lately prototyping new SW with QT4 and I have some thoughts about mobile UIs. The QT was originally developed for desktops, so it doesn’t yet have all features required for mobile UI’s. The current literature about QT4 is not very well suitable for mobile development, since the books mainly focus on desktop UI programming. Phones with small screens are very different environment, and you should design the UI very carefully before implementing it.  

### Tabs   
Tabs are widely used in desktop environment, and I’m not sure how well they fit in mobile devices. It’s already possible to do tabs in S60 Avkon UI, so it should be OK with QT too.  

### Using different windows/views
In S60 we have views based architecture architecture. Using different views in mobile SW feels like a pretty good idea to me. Most of S60 software uses views, and it’s working really well with small displays. Perhaps you don’t have to create many views with devices equipped with large screen like Nokia’s tablets with Maemo, but for S60 3.x devices you definitely should use views for them.  
In QT4 the views can be implemented with QMainWindow, The QMainWindow can have one menu and several widgets on it. Changing the view is easy, just change the mainwindow on the screen, by deleting the old one, or calling hide() function when you want to change view.  

### Using keys**  
All QT4 enabled devices doesn’t have touch screen, so you should also make it possible to use the application with keys only.  

### Different orientations 
The S60 devices can often change orientations. For example the 5800 express music can be used in portrait or landscape mode. I’m not sure if there is a way to change orientation in current QT 4.5 release. At least I didn’t find it.  

### Adapting into different resolutions
Currently S60 3.x phones have 240 x 320 resolution and 5.0 phones have 640 x 360 resolution, and maemo is 800 x 480. The application should scale into all of there solutions, plus it should be usable in portrait and landscape modes. One way of handling this issue, is to make a separate ui design for each resolution, and orientation, which takes a lot of work with small application.  
The other solutions is to dynamically look at devices resolution and scale all the widgets according to the current resolution, but I think that UI optimization with separate UI design can provide better user experience.  

### Menus 
In S60 Qt4 version you can have one menu for each QMainWindow. However I don’t think that menus are good for touch screen devices, since it’s more intuitive just to click different objects. Checking menus in different views is not very good convenient, if you are using touch. The menu might be even confusing with touch devices, since you should press a button in each view to see what’s hidden in the menu.  
The menus could be very usable for games &amp; emulators. You could pause the game by pressing menu, and then go into the settings etc. And there is basically only one main view in the game programs plus settings views. The settings views can even share the same menu, so they shouldn’t be too confusing.  

### Different UI for touch screen devices
In current S60 devices touch enabled 5th edition phones have bigger resolution than 3.x based non touch devices. I don’t know if the are going to add touch to the low resolution phones in the future, but currently it feels like you should desing two separate UI systems with QT, if you wan to run your application in both devices. One for the touch, and the other one (with menus) for phones without touch, since menu might be optimal solution in some cases for non touch devices.
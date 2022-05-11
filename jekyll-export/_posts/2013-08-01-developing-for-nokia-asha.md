---
id: 4536
title: 'Developing for Nokia Asha'
date: '2013-08-01T00:31:02+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=4536'
permalink: /4536/
categories:
    - 'J2ME Development'
tags:
    - asha
    - J2ME
---

Nokia started a Premium Developer Program for Nokia Asha phones [http://developer.nokia.com/Developer\_Programs/Asha\_developer\_program.xhtml](http://developer.nokia.com/Developer_Programs/Asha_developer_program.xhtml) Where you can get a free Asha phone, if you publish at least one app at Nokia store for Asha in the next 6 moths. I was curious about Asha development, and since they offered a free phone for it I couldn’t resist the offer. So here’s a short summary of my experiences with Nokia’s Asha SDK.  
I got Nokia Asha 310 from the developer program, so I wanted to keep that as a primary device, and support the new Asha 501. Luckily the apps written with the Nokia Series 40 Developer SDK 2.0 are compatible with the new Asha 501. You just need to support the lower resolution of Asha 501, and that’s it. I’m now targeting the S40 full touch Asha phones with resolution of 240×400 and the new Nokia Asha phones with the resolution of 240×320.

### IDE

The IDE is build on top of Eclipse, so it feels familiar to any Eclipse user. (Carbide). It has basic project templates etc. so you’ll get a pretty nice project created by creating a new J2ME project from the IDE. However the default template doesn’t give your app a default icon, and it doesn’t set any icons into the manifest file. This is a big headache for Asha noobies, since you can not install the app into the phone if it’s missing the icon &amp; definitions in the manifest file. However you can debug and run your application on the emulator without these, so it’s really confusing.  
Now-days every single SDK adds icons and does all the packing magic to the new projects, so you can run your hello world application on a phone, by just pressing run. Just see Android, iOS, BlackBerry, Windows Phone SDKs. This is definitely something that Nokia should fix.  
**On Device Debugging**  
This one was really hard to get working. You can download all the tools needed from Nokia developer website: [http://developer.nokia.com/Develop/asha/java/start/On-Device\_Debugging/](http://developer.nokia.com/Develop/asha/java/start/On-Device_Debugging/) However I never managed to get the Debugging working though Bluetooth connection, so I had to use the USB cable for debugging. The biggest issue for me with the debugging was the project created just didn’t start with my new project. Later on I learned that I must have an icon for the app before I can install it to the phone ( I whined about this already in the IDE chapter).

### J2ME

J2ME is really an old platform. It’s roots starts from 1998 when Sun focused on mobile platforms. It offers a subset from Java made for Mobile devices. Now Android is running full Java stack, and its own UI stuff on top of the java, so the old J2ME feels really outdated. The worst part is the UI. It reminds Nokia’s Avkon UI framework from Symbian. You’re filling out menu items and the views from the code, while in all “new” UI frameworks you have some declarative way of defining the UIs look. XML in Android, XAML in Windows Phone, and QML in Qt. Writing a UI for Asha is not a pleasant task.

### Publishing to the Nokia Store

The publishing process was pretty much the same as publishing a Symbian application. The Web UI for publishing an app is already familiar, so no complaints about the UI. The process is similar to Symbian sis files. So the developer uploads the application unsigned, and then Nokia will sign the application before putting it into the Nokia store.  
However the certification Criteria for J2ME application are ridiculous. You can get the list of requirements at [http://javaverified.com/graphics/PDF/UTC\_3\_0\_FINAL.pdf](http://javaverified.com/graphics/PDF/UTC_3_0_FINAL.pdf) It’s really my fault for not reading the certification document list carefully though at the first app submission, but there are some pretty odd requirements.  
For example your app must have a help / instructions item on the menu, and it must provide instructions to the user. WTF. What year is this? Have you seen any instructions in any iOS / Android / Windows Phone application? No? Because there are no instructions. The common UI design pattern is to make apps so easy to use, that the user can discover how the app is used by him/herself.  
Well, after implementing the Help item into menu, and writing some general instructions my app got passed the java verified, and I got my application into the Nokia store.
---
id: 4053
title: 'BlackBerry Got Game Port-a-Thon'
date: '2012-11-20T16:29:54+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=4053'
permalink: /4053/
categories:
    - 'BlackBerry10 Development'
tags:
    - appworld
    - bb10
    - 'Qt Development'
---

Last weekend I participated to the BlackBerry’s Got Game Port-a-Thon even. It was a 36 hours event, and the goal was to submit as many games as possible to the BlackBerry’s app world.  
The *new* BB10 OS has a tool to repack Android and HTML5 applications, so I expected that most of the participants will do just that. The new BB10 is Qt based, so I thought that porting existing Qt apps is probably quite easy, but it’s not as straight forward as repackaging old apps, so I decided to do just that (hopefully less competition with this approach). I ported few QWidget and QML based apps just for the fun 😉

#### Porting Qt apps with BlackBerry 10 NDK

I had 36 hours time to port apps in an environment that I had never used, so it was really important to learn how to use these new tools quickly. Luckily I can say that the BB10 native SDK is really good! The whole SDK is build on top of Eclipse based UI, and that’s pretty easy to use. It has a lot of project templates to choose from, and creating new installation packages from “file/export” is really easy.  
The BB10 simulator is basically a x86 compiled image of the Operating System running on VmWare! This is how you should create all of you simulators. I’m looking at you Android. Booting up the simulator takes only few seconds, and launching new apps on the simulator is really fast.  
Locking the orientation in BB10 apps is quite easy. Just add these few lines into the application bar-description.xml file.

```
<initialWindow>
<aspectRatio>portrait</aspectRatio>
<autoOrients>false</autoOrients>
</initialWindow>
```

The NDK isn’t perfect, it has at least one strange “feature” on it. if you’re using console.log(); in your qml file, the log output doesn’t go into the console, instead it goes into the terminal. You can view the terminal output by right clicking the simulator connection, and clicking “SSH connect”. In the SSH connection window you should type

```
slog2info -w
```

36 hours is not much time, so I wanted to make a simple quick process to port new apps. Here’s the process that I used

1. Create new Cascades based project from the BB10 project templates. This way I got all the necessary Qt-library dependencies into the bar-description.xml file
2. edit the bar-description.xml and add author name, application description etc.
3. add qrc-file as a resource to the projects .pro file( I used resource-file, since it’s more portable)
4. remove main.cpp and app.cpp files from the project( I’m going to use the original sources instead)
5. add all sources and resources from the project that you’re porting
6. compile and link
7. debug, hack, debug, etc.

#### My Ports

I managed to make complete six somewhat working games to the BB10. I made these port in a hurry (see the process above), so the code really is not clean enough to push for the original author / repositories. I have no idea if they will never qualify for the BB appworld, but here are the github repos, in the case that you’re curious and want to compile them by yourself 🙂 Maybe I can build some developer packages of them and share them in here, if they don’t qualify to the appworld.  
I made following ports:

- FreeJeweled: <https://github.com/Summeli/FreeJeweled>
- qmlSokoban: <https://github.com/Summeli/qmlSokoban>
- Heebo: <https://github.com/Summeli/Heebo>
- Blubbles: <https://github.com/Summeli/Blubbels>
- NetWalkMobile: <https://github.com/Summeli/NetwalkMobile>
- NineMen’s Morris: <https://github.com/Summeli/NineMensMorris>
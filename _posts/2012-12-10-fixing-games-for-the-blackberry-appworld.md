---
id: 4129
title: 'Fixing games for the BlackBerry AppWorld'
date: '2012-12-10T16:56:26+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=4129'
permalink: /4129/
categories:
    - 'BlackBerry10 Development'
tags:
    - bb10
    - Blubbels
    - FreeJeweled
    - qmlSokoban
---

I have fixed the games I submitted to the BlackBerry Game-Port-A-Thon. I had many bugs reported by the AppWorld team that occurred only on the BlackBerry DevAlpha device, but not on the simulator. It seems that the DevAlpha is very important tool, if you want to develop for the upcoming BB10 phones.

#### FreeJeweled

This one was the trickiest. I don’t own a DevAlpha, and yet I developed for it. The game seemed to work really well on the simulator, but it didn’t work as well on the real device. Luckily I got some images from the BlackBerry AppWorld testing team to help me with my development.

![FreeJeweled running on DevAlpha device. Screen shot provided by BlackBerry Appworld team](/wp-content/uploads/2012/12/freeJeweledBug1-180x300.jpg)

![FreeJeweled running on simulator](/wp-content/uploads/2012/12/free_jeweled_bug_simulator-179x300.png)

As you can see the game worked really well on the simulator, and badly on the real device. At first I thought that my problem was that the size of the menu bar buttons is based on the jewel size from the game, and those values came from c++ engine. I thought that maybe there’s some very strange timing issues or something… and that’s causing the qml side ending up with some strange default values. My first attempt was hardcoding the button sizes, but I still got rejected from AppWorld, and they told me that it still looks just as bad.  
The FreeJeweled is using custom fonts which are packaged into the application itself. My second guess was that the fonts are not working in the same way on the real device as they are on the simulator. This time I had help from a friend with BlackBerry DevAlpha to run some tests for me, and it turns out that the problem was with the font behavior. I blindly changed font sizes on my code, and sent a package for him to test, and after couple of packages we finally got it right.  
  
Below you can see the working version of the game running on the DevAlpha, and running on Simulator.

![FreeJeweled running on Dev Alpha](/wp-content/uploads/2012/12/freejeweled_working_device-180x300.png)

![Working version of FreeJeweled runnin on simulator](/wp-content/uploads/2012/12/free_jeweled_working_simulator-180x300.png)

It seems that I really need the DevAlpha device if I want to do quality ports, since things like this tend to happen sometimes.

#### Blubbles

Blubbles was running really smoothly on my simulator, but it didn’t work on the DevAlpha. I used Qt’s setGeometry function to set the QWidget into the right place on the screen. It worked really well on the simulator, and it left only small black borders on both sides of the application, but it didn’t work at all on the real device. I strongly recommend not to use the setGeometry function in your apps (if you don’t have DevAlpha), since it is working differently on the device, and the on simulator.

```
<pre class="wp-block-preformatted"><pre class="brush: cpp; title: ; notranslate" title="">
//This didn't work out at all
setGeometry(40,0,1200,720);

```

[Blubbels running on DevAlpha](/wp-content/uploads/2012/12/blubbels_bug.jpg) 
  

My solution was to run the App in full screen with:

```
  MainWindow *mw = new MainWindow;
  showFullScreen();
```

  
I also commented out the set Geometry function since it didn’t work. After that I also decided to run the game in portrait mode instead of landscape, and I also modifies the code a bit, so I could get the screen full of bubbles. Now it’s running really well on the simulator, and on the real device too. See the image

[Fixed version of Blubbles, screen full of bubbles](/wp-content/uploads/2012/12/blubbles_working-183x300.png)
After this I got one more rejection from the AppWorld. It turns out that I left a link to the original Blubbles project at source forge, and I had to remove it, since it was against the BlackBerry AppWorld policies. They categorised the sourceforge as “Another app store”, and told me to remove the link. It’s really not an issue for me, since they still agreed that I could keep the link to my github page where I host the source code. I’m fine with the “github only” policy, since the source code is still easy to find for anyone who’s interested about it.

#### qmlSokoban

For this game I got a very valid point from the AppWorld testes that the man is impossible the move. Actually it was possible to move the man, but you just had to click the next block of the screen where the man is. Dragging event’s with a finger moved only the world around the man(not the man itself). I guess that this happens all the time with the real device and touchscreen. The controls are easy only with the mouse, but they don’t work that well with the touchscreen.  
I decided to add a DPAD to control the man. I still wanted to keep the sokoban controls “clean” in the way that no one will mess up their game by an accidental move. Therefore, I configured the buttons to only control the character from “mouseClick’s”, and not from drag events. The character moves now only with one “tap” to the DPAD. The character will not move two screens even if you keep the finger pressed to the button(this to prevent accidental moves). The AppWorld testers also agreed that this was a good fix, and I got the game passed to the store.  
Here’s a snippet how to create “tapping” DPAD buttons for your game. You only need one image component, with proper anchors.

```
//qml-code for one controller button
Image {
 id: up
 source: "./images/controller/up.png"
 anchors.top: parent.top
 anchors.horizontalCenter: parent.horizontalCenter
 MouseArea {
   anchors.fill: parent
   onClicked: { Game.moveUp(); }
   }
 }
```

![qlmSokoban with D-PAD<](/wp-content/uploads/2012/12/qmlSokoban-300x184.png)
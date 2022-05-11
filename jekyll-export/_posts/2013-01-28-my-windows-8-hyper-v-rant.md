---
id: 4085
title: 'My Windows 8 / Hyper-V Rant'
date: '2013-01-28T14:06:14+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=4085'
permalink: /4085/
categories:
    - 'Windows Phone Development'
tags:
    - hyper-v
    - wp8
---

The new lumia phones are looking really good, and I wanted to develop something for it. I started by porting a cocos2d-x game, and I also won a Lumia 820 with my forum.nokia [cocos2d-x porting entry](http://www.developer.nokia.com/Community/Wiki/Creating_a_New_Cocos2d-x_Project_for_Windows_Phone_8).  
To develop for wp8 you’ll need the Windows 8 Pro edition. It costs only about 30 EURs, so it’s kind of no brainer to buy it. The biggest issue for me with wp8 is that the emulator is build on top of Microsoft’s own virtualization platform called Hyper-V.

#### Hyper-v

The [Hyper-V](http://en.wikipedia.org/wiki/Hyper-V) is a windows virtualization service that give you an opportunity to run different operating system under the virtualization service. It gives you pretty much the same features as VM-Ware, or Virtual Box, but it’s built as windows service, so you could run multiple operating systems inside that one service.

#### The Hyper-V steals the virtualization extensions from your processor

This is pretty irritating. The Hyper-V is a service (starts on windows startup) that takes my processors virtualization extensions into use so I can not run any other virtualization software when I have this crap enabled. For example BlackBerry emulator is running on top of VM-Ware, and it can not be used while the Hyper-V is enabled. I also like to develop for Linux with Ubuntu running on Virtual-Box, but that’s also not going to happen with Hyper-V enabled 🙁

#### You need to boot twice after enabling/disabling Hyper-V

This is also very annoying, since I have to constantly disable / enable the Hyper-V when developing for other platforms than wp8. After disabling the Hyper-V your pc will boot, and on that boot you’ll get “configuring windows features” dialog, and after that the PC will boot once more with the new config that has Hyper-V enabled/disabled.

#### Microphone input does not work

This is true WTF material. The microphone input on my motherboard doesn’t work after enabling hyper-v. It has a lot of staic noise, and it’s normal again when I’m disabling Hyper-V. I bough a USB-microphone to solve this issue. However running any other virtual machines like VM-ware does nothing to the mic input. I have no idea what the Hyper-V is doing…

#### Enabling the Network connection on the emulator disconnects the desktop

Another WTF. If I enable the network connection on the windows phone emulator, then the network connection drops from my desktop PC. Developing app that requires a network connection is not feasible with the current emulator.

#### Turning the Hyper-V off

This is the most important feature. You can turn it off. After this the wp8 emulator doesn’t work, but you can still build for ARM and test on device.  
Turn the Hyper-V off by opening the control panel -&gt; add/remove programs -&gt; configure windows features, and then uncheck the Hyper-V box.

<div class="wp-caption aligncenter" id="attachment_4120" style="width: 310px">[![](http://www.summeli.com/wp-content/uploads/2012/11/remove_hyper_v-300x264.png "remove hyper-v")](http://www.summeli.com/wp-content/uploads/2012/11/remove_hyper_v.png)Remove hyper-v

</div>
---
id: 18
title: 'Starting Maemo and QT4 development'
date: '2008-12-02T16:39:23+02:00'
author: Summeli
layout: post
guid: 'http://koti.kapsi.fi/~summeli/blog/?p=18'
permalink: /18/
aktt_notify_twitter:
    - 'yes'
categories:
    - 'Qt Development'
tags:
    - eclipse
    - Qt4
    - VmWare
---

I have been working with [Maemo ](http://maemo.org/)platform for couple of weeks, and I wanted to share few tips for starting the development. It’s not as easy to start with as S60 😉 But it’s an open platform and you can find a lot of source( and binary) for it, so developing you own applications are quite fast. Really fast with QT actually 🙂 Actually I wanted to learn QT and try running apps developed with qt in ARM, since it’s coming to S60 too. The S60 QT will be QT embedded, so it will have a bit more features, than the regular QT, which is currently ported to Maemo. Currently there is already QT[ preview available for S60](http://trolltech.com/developer/technical-preview-qt-for-s60)  
**The SDK installation:**  
For windows environment one must first install a virtual machine to run Linux in. I tested both VmWare and VirtualBox. The VmWare is a lot easier to install, if you have a premade image. However the VirtualBox can take snapshots from file system, which can be used for recovering the fully installed development environment, if you will broke it by accident.  
In Linux, the first step would be to install [Maemo.](http://maemo.org/)  
First install the Scratchbox and the install the Maemo SDK. I recommend using the ready scripts.  
I also found Memo SDK VMWare image at <http://maemovmware.garage.maemo.org/>. It pretty much contains everything required for Maemo development. Eclipse, Maemo SDK, image creation scripts etc. I really recommend using this image; it even has[ EsBox eclipse plug-in](http://esbox.garage.maemo.org/index.html) for Maemo development pre-integrated.  
As default the Scratchbox is in ARMEL state. It can be changed into X86 state with command “sb-menu” and then select X86 environment.  
The QT4 can be installed after Maemo. Add the repositories listed at [Qt Maemo website](http://qt4.garage.maemo.org/diablo.html). Then install qt packages by typing in the Scratchbox shell

```
<pre class="brush: css; title: ; notranslate" title="">
apt-get update
apt-get install libqtcore4 libqtgui4 libqt4-network
apt-get install libqt4-dev qt4-dev-tools qt4-qtconfig
```

currently the Qt4 build seems to be working at X86 environment, but it doesn’t compile in there. However it doesn’t work in armel environment, but you can compile a working version by yourself 🙂  
**TIPS**  
And now everything is installed. My first problem with Maemo devepment was creating the packages. In Symbian it’s very easy to create sis files with pkg-files and all. In Maemo debian packaging system is used. A very good tutorial for packaging applications with qt and Maemo can be found from [Maemo Wiki](http://wiki.maemo.org/Packaging_a_Qt_application).  
On common tip for building applications: use “–prefix=/usr/” argument for configure and cmake to get application directories correct. I learned this through trial and error.  
Moving files between source and scratchbox:  
create directory in scratchbox side, which will be binded to the host side, for example directory host. Create a binding directory also in the host side. Then bind the directories between host and scratchbox, by bind command in the host side:

```
<pre class="brush: css; title: ; notranslate" title="">
sudo mount --bind bind_dir /scratchbox/users/usrname/home/usrnamel/host/
```
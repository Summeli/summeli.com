---
id: 1451
title: 'Implementing AntSnes with Qt part 1: Creating Views'
date: '2010-01-15T19:46:19+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1451'
permalink: /1451/
aktt_tweeted:
    - '1'
aktt_notify_twitter:
    - 'yes'
categories:
    - 'Qt Development'
    - 'Symbian Development'
tags:
    - AntSnesQtDev
    - 'Qt Development'
    - Symbian
---

This is first post on Qt App development series on Symbian. In this series I will describe how I made a new user interface with Qt for AntSnes. The same Ui will be later be used with gpsp and psx4all.  
The mobile UI should be pretty much different, than the desktop UI, so there are some challenges ahed. I’m still sure that the UI will be a lot cooler than the old AntSnes UI with Symbian Avkon layer.  
The UI will made with two separate views. The emulation view, and the settings view. The are both inherited from the QMainWidget, and they both are controlled by viewcontroller-class. The ViewController is only responsible to call hide() and show() functions to widgets, so there’s allways the correct view shown on the screen.  
Here’s an example how the app is started with the viewcontroller class.

```
int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    ViewController* vc = new ViewController();
    return a.exec();
}
```

  
Let’s create two views at viewcontroller’s constructor

```
ViewController::ViewController()
{
    emuView = new AntSnesQt();
    emuView->hide();
    settingsView = new EmuSettings();
    settingsView->show();
}
```

An example how the ViewController is changing the current view:

```
ViewController::showSettings()
{
	emuView->hide();
	settingsView->show();
}
```

I decided to make the app to support only landscape orientation for 5th edition devices (for obious reasons), so I need to forse the orientaiton to the landscape mode. Here’s a tip how it’s done on Symbian. [http://wiki.forum.nokia.com/index.php/CS001517\_-\_Lock\_application\_orientation\_in\_Qt\_for\_Symbian](http://wiki.forum.nokia.com/index.php/CS001517_-_Lock_application_orientation_in_Qt_for_Symbian) This is first Symbian dependent part of my application. There will be few more Symbian specific implementations, but my goal is to keep the application as close to the vanilla Qt, as possible. I want to keep the door open to the Maemo platform as well 🙂
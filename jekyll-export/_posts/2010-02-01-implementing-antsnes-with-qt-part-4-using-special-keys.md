---
id: 1488
title: 'Implementing AntSnes with Qt part 4: using special keys'
date: '2010-02-01T22:15:29+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1488'
permalink: /1488/
aktt_tweeted:
    - '1'
aktt_notify_twitter:
    - 'yes'
categories:
    - 'Qt Development'
    - 'Symbian Development'
tags:
    - AntSnesQtDev
    - buttons
    - 'Qt Development'
    - SwEvent
    - Symbian
---

### Support for green, red, menu, and camera keys:   

Current S60 v. 5.0 phones really don’t have that much keys, so I decided to add support for all keys that I can find from the phone. This will require the SwEvent capability. The downside is that SwEvent requires signing by user. The signing can be made at [Symbian signed website.](https://www.symbiansigned.com/app/page/public/openSignedOnline.do)  
Here’s a trick how to catch these special button events from the phone.

```
<pre class="brush: cpp; title: ; notranslate" title="">
CAknAppUi* appUi = dynamic_cast<CAknAppUi*> (CEikonEnv::Static()->AppUi());
TRAPD(error,
    if (appUi) {
     // disable other green key functionality to be able to use it
     appUi->SetKeyEventFlags(CAknAppUi::EDisableSendKeyShort|CAknAppUi::EDisableSendKeyLong);
    }
//capturing menukeys, redkey (no), and camera keys
iMenuKeyHandle = CEikonEnv::Static()->RootWin().CaptureKeyUpAndDowns(EStdKeyApplication0, 0,0);
iNoKeyHandle = CEikonEnv::Static()->RootWin().CaptureKeyUpAndDowns(EStdKeyNo, 0, 0);
iNoKeyHandle2 = CEikonEnv::Static()->RootWin().CaptureKey( EKeyNo, 0, 0 );
iCameraKeyHandle = CEikonEnv::Static()->RootWin().CaptureKey( EKeyDevice7, 0, 0 );
```

There are limitations in these keys also. The green and red button are sending the KeyUp events, even if I would hold the button down. So these keys shouldn’t be mapped into keys that require long key presses.  
### Adding support for multimedia buttons:

There’s are very good forum.nokia article about how to utilize multimedia keys: [http://wiki.forum.nokia.com/index.php/TSS000432\_-\_Utilising\_media\_keys](http://wiki.forum.nokia.com/index.php/TSS000432_-_Utilising_media_keys). I utilized the multimedia keys in similar ways, and after that I’ll make a KeyEvent with Qt’s Event:

```
QKeyEvent *event = NULL;
event =  QKeyEvent::createExtendedKeyEvent( QEvent::KeyPress, KPlayButtonPress, Qt::NoModifier,
 KPlayButtonPress, KPlayButtonPress,Qt::NoModifier);
QCoreApplication::postEvent (receiver, event);
```

These event’s can be sent to the receiver object, which can use the key events as any other normal keys. However multimedia keys also have some limitations 🙂 The play and stop keys are not sending the keyup events at all. Therefore I had to set a initial time how much it takes until the keyup event is generated. Initially I set the timeout to 80ms. It seems to be working quite well 🙂  

### Summary about button limitations:

For red/green keys the user must sign the application in symbian signed, or I have to buy a cert and get the applicaiton signed. I’m probably not going to do that, so it’s more work for the user.  
Currently there are four buttons that doesn’t support long key presses. I tested these only with my N97. Other phones might behave differently.  
green/red buttons: automatic keyup event after some time  
play/stop button: automatic keyup event after 80ms.
---
id: 296
title: 'Collection of S60 UI tricks'
date: '2009-02-17T12:06:40+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=296'
permalink: /296/
aktt_notify_twitter:
    - 'no'
categories:
    - 'Symbian Development'
tags:
    - backlight
    - S60
---

I’m currently busy with the next AntSnes release. Here is some S60 UI ticks I used in the previous AntSnes v0.3 release.  
Starting a menupane at app startup.

```
//at AppUI ConstructL
CEikonEnv::Static()->AppUiFactory()->MenuBar()->TryDisplayMenuBarL();
```

Keeping the backlight on.

```
//call this often enough. For example once in each second
User::ResetInactivityTime(); //keep the backlight on
```

Catching events when menubar is opened, or cancelled/closed, so we can stop and start the emulation again.

```
//See when menu was launched in here
void CAntSnesAppUi::DynInitMenuPaneL( TInt aResourceId, CEikMenuPane* aMenuPane )
{
    if( aResourceId == R_MENU ) //if R_MENU, then the menupane was launched
    {
        PauseEmulation();
        iMenuOpen = ETrue;
    }
}

// Handle key events, see if it was a cancel event and menubar flag was on
// ESCAPE cancels loading or saving
TKeyResponse CAntSnesAppUi::HandleKeyEventL(const TKeyEvent aKeyEvent,TEventCode aType)
{
    if( aKeyEvent.iScanCode == EStdKeyDevice1 and iMenuOpen )
    {
        //The menu is cancelled, continue emulation
        continueEmulation();
        iMenuOpen = EFalse;
    }
    return EKeyWasNotConsumed;
}
//The some command was chosen from menubar, disable flag, and continiue emulation
void CAntSnesAppUi::HandleCommandL(TInt aCommand)
{
    iMenuOpen = EFalse;
    continueEmulation();
}
```
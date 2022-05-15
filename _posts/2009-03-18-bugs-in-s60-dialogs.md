---
id: 440
title: 'Bugs in S60 Dialogs'
date: '2009-03-18T22:01:36+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=440'
permalink: /440/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - CAknNoteDialog
    - S60
---

I found this when trying to get AntSnes remembering the last used directory. It was actually really simple and everything worked according to S60 documentation with N96, but N95-2 had some SW bugs on dialogs.

```
selected = AknCommonDialogs::RunSelectDlgLD(ptr,_L(E:\\SnesRoms\\),R_MEMORY_SELECTION_DIALOG, R_LOAD_ROM_DIALOG);
```

In N95-2 the code goes to the E root, like it wouldn’t find any roms under roms directory. Maybe firmware update helps…  
I also had some problems in the past with CAknNoteDialog and capturing the key that was pressed to dismissing the dialog. According to S60 docs it should have worked, but it didn’t. My solution was to create my own Dialog class for the key config. It’s really hacked together in few minutes, but it’s good enough for the purpose (it’s not going into any platform, but it does what is shoud :).

```
class CAntKeyDialog : public CAknNoteDialog
{
public:
CAntKeyDialog(const TTone aTone, const TTimeout aTimeout);
        ~CAntKeyDialog();
    TInt RunKeyDialogLD( const TDesC; aText);
private:
    TKeyResponse OfferKeyEventL(const TKeyEvent aKeyEvent,TEventCode aType);
    TInt iKeyScanCode;
    CActiveSchedulerWait* iWait;
};
CAntKeyDialog ::CAntKeyDialog(const TTone aTone, const TTimeout aTimeout)
:CAknNoteDialog(aTone,aTimeout)
    {
    }
//just overwrite the default function :)
TKeyResponse CAntKeyDialog::OfferKeyEventL(const TKeyEvent aKeyEvent,TEventCode aType)
{
    if( aType == EEventKeyDown)
        {
        //save the scancode
        if( aKeyEvent.iScanCode == EStdKeyDevice1 || aKeyEvent.iScanCode == 1)
        	{
        	//skip
        	iKeyScanCode = 0;
        	}
        else
        	iKeyScanCode = aKeyEvent.iScanCode;
        iWait->AsyncStop();
        StaticDeleteL(this);
        }
   return EKeyWasConsumed;
}
//just overwrite the default function :)
TInt CAntKeyDialog::RunKeyDialogLD( const TDesC aText)
    {
    if( iWait )
    	{
    	delete iWait;
    	iWait = NULL;
    	}
    iWait = new (ELeave) CActiveSchedulerWait();
    CAknNoteDialog::SetTextL( aText );
    CAknNoteDialog::ExecuteDlgLD( R_INFORM_USER );
    iWait->Start();
    delete iWait;
    iWait = NULL;
    return iKeyScanCode;
    }
```

Using the dialog class is pretty simple. The S60 documentation promised the CAknNoteDialog to work in this way too…

```
dialog = new (ELeave) CAntKeyDialog(CAknNoteDialog::ENoTone,CAknNoteDialog::ENoTimeout);
iSettings.iScanKeyTable[11] = dialog->RunKeyDialogLD( *textResource);
```
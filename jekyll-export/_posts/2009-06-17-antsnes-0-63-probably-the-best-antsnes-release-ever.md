---
id: 845
title: 'AntSnes 0.63 &#8211; Probably the best AntSnes release ever'
date: '2009-06-17T22:42:05+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=845'
permalink: /845/
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
aktt_tweeted:
    - '1'
categories:
    - 'S60 3rd edition'
tags:
    - AntSnes
    - N95
    - N96
---

AntSnes is a Snes9x port to S60 3.x. This is the best release since 04. Thanks to Mirek for testing 😉  
Changed in 0.63 vs. 0.61

- The “remember last ROM directory” feature was removed, since it seems to be causing serious issues in some phones. If the “last rom directory” feature worked in your phone with previous releases, then you can download the older 0.62 release.

Whats new:

- Battery saves
- New fancy icon
- savestate bug fixed. 0.5 users see known issues!
- Modified key config. All 0.5 version users must update the key config after this Release.  
    After settings the screen to the N-gage mode the user must set keys again, since the S60 keypad doesn’t know that feature. The update was made for E75 users, who might not have the d-pad mapped for arrow keys
- Localization for: Danish, Hungarian, Indonesian, Brazilian Portuguese and Russian besides the English.
- Don’t like the localization? No prob. You can just download the English only package too.

know issues:

- Audio still sucks!
- due to a bug in previous 0.5 version the save/load slot places have changed. Try to find you own correct save slot. Doesn’t affect to users who haven’t used the previous version..
- There are still some issues in localization

Thanks for the localization goes to following persons:

- Danish 07 by: Jens kikkenborg
- Hungarian 17 by: Attila Molnár
- Indonesian 59 by: Antok
- Brazilian Portuguese 76 by: Rodrigo Carus
- Russian 16 – Chepelev Anton
- Polish 27 – Krzysztof Urbanowicz
- Bulgarian 36 – Lil Stenly

Did you want to make translation for your own native language, but missed AntSnes release 0.6? Don’t worry, you’ll get a new chance later when I’m making a port for the S60 5th edition.  
  
### Installation: 
Just download and install.  
If you got an error “unable to install”, or “certificate error” you might be having problems with the certificate. See my other blog post about two common fixes for this. [Fixing self-signed certificate related problems](/932)  

### Video settings: 
Video Renderers: A restart is required after video renderer has been changed

- DirectScreenAccess -Default, works in every phone
- OpenGL ES 1.1 – Renders snes frames in full screen. Requires OpenGL ES 1.1, so it doesn’t work in all devices.

Screen Orientatuions: A restart is required after orientation has been changed

- portrait – Default
- Landscape – Normal landscape
- N-Gage – landscape, but image is upside down. It’s meant for phones with “n-gage mode” like N95 and N96. The N96 can use the multimediakeys by default, but N95 users must use [Magic keys](http://www.symbian-freak.com/downloads/freeware/cat_s60_3rd/descriptions/systools/magic_keys_remap_and_extend_your_keyboard.htm) to map keys 1-4 to multimediakeys.

Frame skip:

- Auto – continually adjust the frame skip speed to make your games play as smooth as possible
- User define speed – some games might not run very well with Auto selection, since the frame rendering might take longer than a frame time with audio frame etc. Feel free to test different options, if you wish.

Show FPS:

- Off – default
- On – Show frames per second on upper left corner.

The Video settings modification takes effect, when AntSnes is started next time( a restart required).

![N96 keymap](/jekyll-export/wp-content/uploads/2009/01/n96_keys-300x198.jpg)

### Audio Settings: 
The Audio isn’t probably working. If you get it working, please post you config, phone and the game 🙂  
Enable Audio: On/Off  
Sample Rate: 8000Hz, 11025Hz, 16000Hz, 22050Hz and 44100Hz can be chosen  
Stereo: On/Off  
Volume: Adjust volume  
Enable SpeedHack: On/Off. The SpeedHack makes audio render a bit faster, but it might cause some errors with some roms.  

### Key config
Start key config to configure keys. The multimediakeys are not supported in the key config, but you can use any normal keys in here. 
 
### Download:  
AntSnes English only: [ AntSnes\_v063\_en.sis (35635 downloads) ](/jekyll-export/wp-content/uploads/2009/10/AntSnes_v063_en.sis)  
AntSnes with localization: [ AntSnes\_v063.sis (8720 downloads) ](/jekyll-export/wp-content/uploads/2009/10/AntSnes_v063.sis)  

sources: [AntSnes\_src\_v0.63.zip](http://www.summeli.com/wp-content/uploads/2009/06/AntSnes_src_v0.63.zip)  
**Update:** The AntSnes is not currently working with 5th edition devices, but the next release will be for the 5th edition. In the meanwhile see my blog post[ The future of AntSnes](/842)  
**Compability:**  
Here it is my new testing rom for your antsnes 0.6.3:  
1\. alien vs predator  
2\. bugs bunny rampage  
3\. batman the revenge joker  
4\. casper  
5\. Contra 3  
6\. dino city  
7\. mobile suit gundam w endless duel  
8\. fatal fury 2  
9\. fifa 97 gold edition (work perect but the control freeze, can’t use the control)  
10\. fifa 98 road to world cup (work perfect but same with fifa 97, the control freeze)  
11\. flashback – the quest for identity  
12\. go go ackman  
13\. goof troop  
14\. hook. Working fine but control doesn’t work  
15\. jim lee wild C.A.T.S govert action team.  
16\. jungle strike  
17\. knight of the round.  
18\. X-men – mutant apocalypse.  
19\. WWF – RAW.  
20\. WWF – wrestlemania.  
21\. Wolvrine – adamantium rage.  
22\. Wolf child.  
23\. Wing commander.  
24\. Urban strike.  
25\. Uncharted water.  
26\. TMNT – tournament fighter.  
27\. Super mario world.  
28\. Super turican 2.  
29\. Adventure island 2.  
30\. Sid Meier Civilization.  
31\. Popeye – tale of teasing witch hag.  
32\. Pilotwings.  
33\. The ninja warrior.  
34\. Mortal kombat.  
35\. Mortal kombat 2.  
36\. Megaman X 3.  
37\. Mechwarrior 3050.  
38\. Mechwarrior.  
39\. Lucky Luke.  
40\. Lion king.  
41\. Legend.  
42\. Zelda – a link to the past.  
43\. Aladdin.  
44\. Cyborg.  
45\. Supermario kart.  
46\. Zombie ate my neighbour.  
47\. TMNT V
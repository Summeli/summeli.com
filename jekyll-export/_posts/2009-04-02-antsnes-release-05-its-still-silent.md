---
id: 391
title: 'AntSnes release 0.5 : It&#8217;s still silent'
date: '2009-04-02T20:40:06+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=391'
permalink: /391/
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
    - S60
---

AntSnes is taking small steps to improve quality and get the audio working. I really have no idea why the audio isn’t working with current version, but it already has some nice updated, so I decided to make another small step. The 0.5 release is ready 🙂  
The audio isn’t working in 0.5 release ( if you get it working with some phone/configuration please let me know too). I’m saying that I’m outsourcing the testing of this SW to the users 🙂 I did not get the audio working, so I’m hoping that someone will.  
However I made a special 0.4 build for you to hear that you are not missing much. The 0.4\_audio version has hard coded audio, so you can listen what the audio should sound like in 0.5 version. As you can probably hear, the audio is really not high priority for current phones.  
Whats new:

- FPS counter (works currently only with direct screen access)
- User can adjust frame skipping
- remembers last rom directory

TODO’s for next release

- Battery saves
- Fix audio

**Installation:**  
Just download and install  
**Video settings:**  
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

<div class="wp-caption alignnone" id="attachment_203" style="width: 310px">![](/wp-content/uploads/2009/01/n96_keys-300x198.jpg)N96 keymap

</div>**Audio Settings:**   
The Audio isn’t probably working. If you get it working, please post you config, phone and the game 🙂  
Enable Audio: On/Off  
Sample Rate: 8000Hz, 11025Hz, 16000Hz, 22050Hz and 44100Hz can be chosen  
Stereo: On/Off  
Volume: Adjust volume  
Enable SpeedHack: On/Off. The SpeedHack makes audio render a bit faster, but it might cause some errors with some roms.  
  
  
**Key config**  
Start key config to configure keys. The multimediakeys are not supported in the key config, but you can use any normal keys in here.  
Download:  
Sis file: [antsnes\_v05.sis](http://www.summeli.com/wp-content/uploads/2009/04/antsnes_v05.sis)  
\[ad\]  
sources: [antsnes\_v05.zip](http://www.summeli.com/wp-content/uploads/2009/04/antsnes_v05.zip)  
Download the 0.4 release with hardcoded audio support  
**NOTE:** if you decide to try 0.4 audio version and you have already have installed 0.5 version, then you have to uninstall 0.5 before downgrading to 0.4 version.  
Sis file: [antsnes\_v04\_audio.sis](http://www.summeli.com/wp-content/uploads/2009/04/antsnes_v04_audio.sis)  
As you can probably hear the audio support is working, but it’s requiring a lot of CPU as anticipated. So it is there, but it’s not usable with every game. Maybe the new 600Mhz phones will run audio smoothly…
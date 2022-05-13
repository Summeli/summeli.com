---
id: 5684
title: 'Updating JamendoFM for Android'
date: '2014-06-04T11:46:55+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=5684'
permalink: /5684/
categories:
    - 'Android Development'
    - 'Web Development'
tags:
    - jamendo
---

I just got new phone Samsung Galaxy S4 and I noticed that the JamendoFM can not play music on it. I’m sure that it worked with some older Android phones, but it turns out that it doesn’t work with the new ones.  
The problem is somehow related to the radiocontrols. Settings the audiosource, and programatically pressing play doesn’t seem to work with Android anynmore so I changed that stuff into Audio object, which seem to be working pretty well with new Androids.  
Here’s my changes with the audio:

```
   /*the old code that doesn't work*/
   /*
    var audio = $("#radiocontrols");
    $("#radiosource").attr("src", sourceUrl);
    audio[0].pause();
    audio[0].load();
    audio[0].play();*/
    //lets do it with Audio object
    try {
    g_myaudio = new Audio(sourceUrl);
    g_myaudio.id = 'playerMyAdio';
    g_myaudio.play();
   } catch (e) {
    alert('no audio support!');
  }
```

I also added the permissions for the lockscreen so the music will continue to play even when the lockscreen is on. The lockscreen permissions can be added though config.xml (phonegap) like this:

```
   <gap:config-file platform="android" parent="/manifest">
      <uses-permission android:name="android.permission.WAKE_LOCK" />
   </gap:config-file>
```
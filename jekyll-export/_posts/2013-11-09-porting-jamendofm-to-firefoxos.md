---
id: 4632
title: 'Porting JamendoFM to FirefoxOS'
date: '2013-11-09T15:21:22+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=4632'
permalink: /4632/
categories:
    - 'Web Development'
tags:
    - firefoxos
    - html5
    - jquery
    - jQueryMobile
---

I just got a new FirefoxOS developer preview phone, so my next step was to make a port for FireFoxOS. It was pretty similar to porting to tizen. I only had to make a manifest file.

### Creating the application manifest file

The file’s name is manifest.webapp, and creating it was pretty easy. I justcopy&amp;pasted the example manifest file from [firefoxOS tutorials](https://developer.mozilla.org/en-US/Apps/Developing/Manifest), and change all the relevan fields.  
Here’s how my manifest looks like:

```
<pre class="brush: jscript; title: ; notranslate" title="">
{
  "name": "JamendoFM",
  "description": "Jamendo radio client for mobile",
  "launch_path": "/index.html",
  "icons": {
    "60": "/img/icon-60.png",
    "128": "/img/icon-128.png"
  },
  "developer": {
    "name": "Antti",
    "url": "http://summeli.fi"
  },
  "permissions": {
    "audio-channel-content":{"description":"Use the audio channel for the music player"}
 },
  "default_locale": "en"
}
```

### Running JamendoFM under Lockscreen

The coolest thing about Firefox OS is that after settings the permission “audio-channel-content” the app runs music even under the lockscreen. This is not (yet) possible on Tizen, or any other HTML5 frameworks.

### jQueryMobile performance

The cool thing is that the jQueryMobile works really well on firefoxOS! The animations are pretty smooth(no where near 60fps though), and there are no artifacts caused by using them, so they’re OK.
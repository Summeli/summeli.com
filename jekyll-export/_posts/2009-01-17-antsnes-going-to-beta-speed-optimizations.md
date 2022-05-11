---
id: 166
title: 'AntSnes going to Beta: speed optimizations'
date: '2009-01-17T18:07:09+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=166'
permalink: /166/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
syntaxhighlighter_encoded:
    - '1'
categories:
    - 'S60 3rd edition'
tags:
    - AntSnes
    - N95
    - N96
    - S60
---

The new version is optimized for speed, which gives a huge performance boost for N96 (it’s nice for N95 too).  
I expect this binary to work with S60 3.1 and 3.2 phones, but I’m planning to add support for 3.0-&gt; phones in the future. Currenlty there is only the landscape mode, but I will make new blitters for portait mode too.

<div class="wp-caption alignnone" id="attachment_203" style="width: 310px">![](/wp-content/uploads/2009/01/n96_keys-300x198.jpg)N96 keymap

</div>N95 users: You still have to map keys 1-4 with Magic keys [as with alpha version.](http://www.summeli.com/?p=28) The Opengl ES support is not included in this release, since DSA rendering is now an option for N95 users too. Howerver I think that the sound support might be possible with OpenGL ES rendering. To be tested..  
Download: [antsnes\_v01](http://www.summeli.com/wp-content/uploads/2009/01/antsnes_v01.sis)  
Source: [antsnes\_src\_v01](http://www.summeli.com/wp-content/uploads/2009/01/antsnes_01.zip)  
Currently there are small fixes in the ASM core for ARM11. Theese could be usefull for Maemo developers 😉
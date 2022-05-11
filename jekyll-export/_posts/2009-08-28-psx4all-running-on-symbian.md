---
id: 1128
title: 'PSX4All running on Symbian'
date: '2009-08-28T18:42:27+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1128'
permalink: /1128/
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
aktt_tweeted:
    - '1'
categories:
    - Video
tags:
    - N95
    - psx4all
---

I’m currently porting gpSP to the Symbian. Psx4all uses pretty much same SDL stuff and same ARM assembly emitter as gpSP. I just took my porting tricks from gpSP and compiled them with psx4all and here is the result. It’s really not fully optimized yet, but you’ll get the idea that it’s not going to run on N95 smoothly 🙂 I still have some other tricks that would speed it up, but not enough.  
It’s just a proof of concept that this emu could be ported to Symbian with moderate effort, but it’s going to require a lot faster CPU. I might take a second look of this after I’ll get the gpSP port finished.  
See the performance by yourself.  
<iframe allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="315" loading="lazy" src="https://www.youtube.com/embed/S8Auh1mkgeA" width="560"></iframe>
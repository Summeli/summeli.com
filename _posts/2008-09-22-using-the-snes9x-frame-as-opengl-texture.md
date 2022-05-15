---
id: 6
title: 'Using the Snes9x frame as opengl texture'
date: '2008-09-22T14:39:02+03:00'
author: Summeli
layout: post
guid: 'http://koti.kapsi.fi/~summeli/blog/?p=6'
permalink: /6/
aktt_notify_twitter:
    - 'yes'
categories:
    - 'Symbian Development'
tags:
    - porting
---

The Opengl ES framework requires that the texture size must be powers of two. My current version outputs 320×208 pixels frames, so they can not be used as textures.

I looked at the porting instructions and it says that GFX.Pitch should point how many bytes there as per frame. With this I should be able to get 256×239 or 256×224 resolutions. It shouldn’t be too hard to add few back scan lines to the image to get it 256×256. My current Snes9x version has some nasty resolution hacks and it doesn’t have any settings for GFX.Pitch (or it doesn’t se it at least). I think that I will try to take out the rendering part from dr. PocketSnes and merge it with my code. It main.cpp defines 320×240 resolution for frames, but the GFX.Pitch is used as expected, so I hope that the rendering part will output 256×240 frames as well.

I’m also going to make a small optimization trick to the current rendering part and see how much I can get with “decent” rendering routine. However I’m still planning to use OpenGL ES for the rendering.

The OpenGL ES based rendering has some advantages over DSA (DirectScreenAccess).

1. Portability: it’s easy to scale up for new resolutions
2. Can use flitters to increase the rendering quality
3. No need to worry about S60 screen rotations

The portability is the key issue in this project. I’m not sure how long I’m going to use my old N95 8gig model. And it’s quite certain that Nokia will also upgrade their screen resolutions up from QVGA and I don’t want to create new screen blitters for each phone.
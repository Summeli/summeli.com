---
id: 6985
title: 'Why is my GPU freezing'
date: '2014-11-12T23:12:28+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=6985'
permalink: /6985/
categories:
    - Tips
tags:
    - gpu
    - memory
---

I bought a new gpu, AMD’s r9 290x. I was a bit surprised after first day since it seemed to be freezing some times. It could run just perfectly for few hours and then \*boom\*, it freezes. I googled the issue a bit and the most common explanations were Power issues and driver problems. I borrowed a new PSU from a friend, and it was still freezing. Reinstalled the drivers couple of times etc.  
After couple of days I was certain that I had a broken GPU. I was also thinking that I have return it and get a new one from the warranty. However leaving an odd error description like “freezes after few hours” might just do nothing, since the maintenance clerk can always say “it works fine in here”.  
I decided that I have to know what’s wrong with the GPU, so I can easily prove that the GPU is broken. I would need something like memtest86 for GPUs. MemtestCL does just that. I just download MemtestCL, and I got memory errors from my GPU. This could have saved so many hours of meaningless debugging! I also left a warranty claim that the memory is broken and you can easily see it by yourself with memtestCL. I got a new GPU the following day!  
Note to self; If I ever have freezing problems with GPU, see if the memory is working with MemtestCL.  
Oh, And remember to use the most current version of MemtestCL found from github:[ https://github.com/ihaque/memtestCL](https://github.com/ihaque/memtestCL)
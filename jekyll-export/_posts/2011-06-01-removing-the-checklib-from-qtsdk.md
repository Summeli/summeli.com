---
id: 2492
title: 'Removing the checklib from QtSDK'
date: '2011-06-01T16:58:50+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2492'
permalink: /2492/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - checklib
    - QtSDK
---

I think that I said enough about the checklib.exe in my [earlier post.](/2171) I just noticed that the checklib.exe is still fighting against my development in QtSDK 1.1 inside the Symbian^3 SDK.  
This time I decided to get rid of the checklib for good. I just created an empty textfile and renamed that into checklib.exe and then I overwrite the original checklib.exe at QtSDK\\Symbian\\SDKs\\Symbian3Qt473\\epoc32\\tools with the dummy checklib.exe I just created.  
Works like a charm. Now back to development –&gt;
---
id: 13423
title: 'Realtime clock data from Alge-timing system'
date: '2019-04-04T14:25:23+03:00'
author: Summeli
layout: post
guid: 'https://www.summeli.com/?p=13423'
permalink: /13423/
categories:
    - 'Google Appengine'
    - 'Web Development'
tags:
    - alge-timing
    - appengine
    - jquery
    - webapp
    - websocket
---

I made all of this stuff into the Finice 2019 ice climbing competition ([www.finice2019.com](http://www.finice2019.com)). The idea is to send the clock timing events into web, so we could use them in the results-office, or we could insert the clock into the video stream during the competition. There’s always some delay in the video stream, so we need a way to add custom delay into the clock. The data is good, but we have to remember to add some delay so the clock and video will be on sync. It would look stupid if the climber get to the top, and the clock has already stopped a few seconds ago.  
Here’s a short video about how all of it works:  
<iframe allowfullscreen="allowfullscreen" frameborder="0" height="315" loading="lazy" src="https://www.youtube.com/embed/7SYG0wvdRCA" width="560"></iframe>  
  
   
[![](/wp-content/uploads/2019/04/finice1.png)](https://www.summeli.com/?attachment_id=13427)  
So the system contains following parts:

1. alge-timing system, and the interface to the PC via Timy (USB) device. Then the PC read the USB, and sends that data into the webserver. The PC software is on my github: h[ttps://github.com/Summeli/algetiming-streamer](https://github.com/Summeli/algetiming-streamer)
2. The web server part. The very simple logic for handling websockets <https://github.com/Summeli/Streaming-clock>
3. The web page to show the clock signal (this is included in the webserver project).
---
id: 4354
title: 'Playing with Boundary&#8217;s Application Monitors'
date: '2013-04-26T09:47:18+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=4354'
permalink: /4354/
categories:
    - TCP/IP
tags:
    - boundary
    - 'Rasberry Pi'
    - virtualbox
---

Boundary offered free Rasberry Pis for testing their Application Monitors. <https://twitter.com/boundary/status/316529581274308608>  
The Boudanry’s service provides monitors for network traffic. It’s really handy service, if you have a big service with 10+ servers at production, and you’re wondering where the bottlenecks are. Then the monitoring service could save you a lot of trouble. You can instantly see that “Machine X” has big latency, so it hast to be the bottleneck for the service, and it should be fixed. I really like statistics, so I might still continue using these with some of my servers, even while I don’t have that much network traffic.

<div class="wp-caption alignnone" id="attachment_4387" style="width: 310px">![](/wp-content/uploads/2013/03/boundary-300x204.png)Boundary Application Monitors

</div>I had an Ubuntu Server installation on VirtualBox, so I thought that cloning the image would be an easy way to get free Rasberry Pi, and it was 😉 Just right-click on the server installation, and click “Clone”, and then choose “Linked Clone” in the cloning configuration.

<div class="wp-caption alignnone" id="attachment_4356" style="width: 176px">![](/wp-content/uploads/2013/03/virtual_box-166x300.png)cloning in virtual box

</div>  
After the cloning I only had to change the host-name, reboot and run the boundary installation scripts. After half an hour I got the new Rasberry PI. I’m not (yet) sure what to do with it, but it’s pretty nice ARM development platform, since I can run and compile via SSH terminal, so it’s really nice development environment for some small ARM hacks.

<div class="wp-caption alignnone" id="attachment_4400" style="width: 179px">![](/wp-content/uploads/2013/04/my_raspberrypi-169x300.jpg)new raspberrypi from Boundary

</div>
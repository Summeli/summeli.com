---
id: 14735
title: 'Updated the LAN routing machine'
date: '2021-11-03T11:58:41+02:00'
author: Summeli
layout: post
guid: 'https://summeli.com/?p=14735'
permalink: /14735/
categories:
    - pfSense
tags:
    - pfsense
---

My old esxi was intalled on single USB dongle, which died (I failed). So I upgraded everything. Changed old HDD’s into SSD and upgraded all software too

Everything is not hosted on Proxmox instead of Esxi.   
Steamcache is not upgraded into lancache [(http://lancache.net/)](http://lancache.net/)  
pfsense is just newer version

Here’s the upgraded network diagram:

![](/wp-content/uploads/2021/11/lan_network_updated-1.png) At times like thes are pretty nice to have a blog to keep track of things to be done. My old[ multirouting post](/11741) still seems to be a good example how to do this.

Lancache.net  
The new version is being run by docker-compose.
´´´
 $ git clone https://github.com/lancachenet/docker-compose lancache  
~ $ cd lancache  
~/lancache $ nano .env  
~/lancache $ sudo docker-compose up -d  
\# =&gt; Configure your router to serve ONLY lancache-dns
´´´

Reading the caches:  
tail -100f lancache/logs/access.log
---
layout: post
title: "Running Lancache with pfSense"
author: Summeli
description: Running Lancache with pfSense"
categories:
    - pfsense
tags:
    - pfsense
    - lancache
---
# Lancache and pfsense
We've been running [lancache]https://lancache.net/) and pfsense for few years. Before lancache we used steamcache, and then made the logical transformation into lancache

## Configuration
We are using three WAN's for routing traffic in the lan party. 

### lancache
Lancache is running on 192.168.0.2, and we're routing all connection from lancache into the internet via WAN2

### player on network
Players are any ip's starting from 192.168.0.10, and we're routing them to the Internet via Gateway group with WAN1 and WAN3.

![](/img/2022/2022_05_steamcache.png)

## Making changes to the configuration
Every time it seems that our mobile internet providers are different. Sometimes one connection works poorly, and it's important to be able to prioritize traffic into that WAN. My problem seems to be that after the changes to connections are behaving even worse than before making these changes.. I have no idea why this happens, but
it seems to be important to restart the lancache docker every time after making any changes to the pfSense routing rules. 

´´´
 sudo docker-compose down
 sudo docker-compose up -d --remove-orphans
´´´

### It's all about dns

If we don't restart the lanche after changing the pfSense routing schemes we're going to end up with broken dns. Even after rebooting and changing we're seeing few dns resolve timeouts. The error log in /logs/error.log if full of these if we don't make the restart. Maybe someone with more network experience could explain why the restart is needed. I have no idea. Maybe some of these connections are still open though different WANs thant the pfSense would like to use, and those connections will fail. 


´´´
2022/05/21 11:51:07 [error] 1996#1996: *409 clientconfig.akamai.steamstatic.com could not be resolved (110: Operation timed out), client: 192.168.0.10, server: , request: "GET /appinfo/440900/sha/50c5ab81a6599dbf1d0ce1e2e341d59d9b2adc67.txt.gz HTTP/1.1", host: "clientconfig.akamai.steamstatic.com"
´´´´

### EA's origin

To get LanCache working with Origin users must remember to disable safe downloads (downloads with TLS) to get the local lancache working.

## Random restarts required

It seems to be stuck at some points. I have no idea why. Reconfiguring pfSense (with same config) and restarting the lancache docker seems to be solving everything.
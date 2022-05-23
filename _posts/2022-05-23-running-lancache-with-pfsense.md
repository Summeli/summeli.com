---
layout: post
title: "Running Lancache with pfSense in 2022"
author: Summeli
description: Running Lancache with pfSense in 2022"
categories:
    - pfsense
tags:
    - pfsense
    - lancache
---

We started the pfSense journey with SteamCache and pfSense. Few years ago we upgraded into [lancache](https://lancache.net/) , which is caching Origin, Battle.net, Windows update in addition to Steam.

## Configuration

We're running three consumer grade mobile internet routers as WAN's on pfsense, and we're routing the LAN into these hotspots. See my other post about the [configuration](/14735).

### pfSense 2.6.0 Update

Routing was completely broken for me after upgrading from 2.5.2 into 2.6.0. I fixed this by going into interfaces / WAN, and uncheckin **Block bogon networks** on the bottom of the page. It's just a random thing I found from [netgate forums](https://forum.netgate.com/topic/169872/upgrade-2-5-2-to-2-6-0-upgrade-success-limiters-not-passing/6)

### Lancache

Lancache is running on 192.168.0.2, and we're routing all connection from lancache into the internet via WAN2.

![](/img/2022/2022_05_router_hw.jpg)

### Players on network

All users get ips starting from 192.168.0.10, and we're routing them to the Internet via Gateway group with WAN1 and WAN3.

![](/img/2022/2022_05_steamcache.png)

## Making changes to the configuration

In every LAN party our mobile internet providers are serving with different quality. Sometimes one connection works poorly, and it's important to be able to prioritize traffic into that WAN.  

After changing the routing rules (new priorization), it seems that we have to restart the lancache docker. Without the restart the connection doesn't seem to be working as expected.

```
 sudo docker-compose down
 sudo docker-compose up -d --remove-orphans
```

### It's all about dns

If we don't restart the lanche after changing the pfSense routing schemes, we're going to end up with broken dns. Even after rebooting, we're seeing few dns resolve timeouts. Maybe there's not enough bandwidth for dns queries? The error log in /logs/error.log if full of these if we don't make the restart. Maybe some of these connections are still open though different WANs thant the pfSense would like to use, and those connections will fail. 


```
2022/05/21 11:51:07 [error] 1996#1996: *409 clientconfig.akamai.steamstatic.com could not be resolved (110: Operation timed out), client: 192.168.0.10, server: , request: "GET /appinfo/440900/sha/50c5ab81a6599dbf1d0ce1e2e341d59d9b2adc67.txt.gz HTTP/1.1", host: "clientconfig.akamai.steamstatic.com"
```

### EA's origin

To get LanCache working with Origin users must remember to disable safe downloads (downloads with TLS) to get the local lancache working.

## Random restarts required

The Inernet connection seems to be stuck for many at some point, and I have no idea why. Reconfiguring pfSense (with same config) and restarting the lancache docker seems to be solving everything.
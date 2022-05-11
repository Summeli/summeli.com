---
id: 11214
title: 'Building a router for LAN party with pfSense and Steam cache'
date: '2017-12-12T18:58:23+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.com/?p=11214'
permalink: /11214/
categories:
    - DevOps
tags:
    - devops
    - esxi
    - firewall
    - linux
    - pfsense
    - router
    - ubuntu
---

We have small LAN-party for about 30 people twice a year. The party takes a place far away from good internet connections. We have to manage with only 4G connections in here. Currently it get really troublesome if we get some game updates to steam etc. since we’re only having one 4G connection witch is shared with 30 people.

## Hardware Dell R210-II

After lurking a while in the [reddit/r/homelab ](https://www.reddit.com/r/homelab/)I decided to buy a cheap Dell R210-II from ebay. The reasoning was;

1. The physical size is decent (I have limited storage space).
2. The CPU has a support for virtualization.
3. Dell provides the customized esxi images, so the installation should be easy
4. 1 PCI-express slot for new NIC, and enough space to run 2 HDDs in RAID-mode.

I also purchased a 1gigabit 4 port Intel NIC from ebay. Those things are also really cheap. They might be Chinese pirate-cards? (the price is incredibly low), but they still do the work.

## Network Configuration

[![](http://www.summeli.com/wp-content/uploads/2017/10/lan_network-270x300.png)](http://www.summeli.com/?attachment_id=11219)  
  
\[ad\]

## VmWare ESXi

Installing the ESXi was pretty easy. I found a ESXi 6.5 image from DELL website. It wasn’t officially supported, but it seems to working just fine with my hardware. According to the reddit’s r/homelab I should also be able to run this thing with a VmWare esxi free license (some enterprise features are missing then). The only limitation is that you can use only one core per VM. However the esxi seems to be only using the 60 day trial period while the machine is ON, so it seems that i’ll get 60 days of LAN usage for free. Should be enough.

## Steam cache

The Steam cache is just a big cache for steam games and windows updates. The basic idea is that we have to download this stuff only once, and after that it just comes from the cache. Installing it is really fast with docker. It’s basically just “docker run steam-cache”. I pretty much followed these instructions for steam cache <https://arstechnica.com/gaming/2017/01/building-a-local-steam-caching-server-to-ease-the-bandwidth-blues/>  
I had some problems with the latest Ubuntu server stable and steam cache docker. It seems that bind also using port 53 by default, so I have to kill it, before I can run the docker on port 53. However this is pretty easy thing to do, and I only have to do it once, so it’s not a problem.

```
<pre class="brush: plain; title: ; notranslate" title="">
sudo docker run --name steamcache --restart=always -d -v /srv/steamcache/data:/data/cache -p 80:80 steamcache/steamcache:latest
sudo docker run --name steamcache-dns --restart=always -d -p 53:53/udp -e STEAMCACHE_IP=192.168.0.2 steamcache/steamcache-dns:latest
```

## pfSense

I downloaded the newest stable version of the pfsense. Configured the dual WAN for it, and set it to load balancing mode with both WAN connections with same priorities. I also configured the DNS in pfSense to point into my steam cache.

## Gameservers

I also set up a [Factorio ](https://factorio.com/)server for the LAN-party. Factorio server can be easily run with docker image.
---
id: 14746
title: 'Routing Steam traffic into sigle WAN (of three)'
date: '2021-11-13T00:16:25+02:00'
author: Summeli
layout: post
guid: 'https://summeli.com/?p=14746'
permalink: /14746/
categories:
    - pfSense
tags:
    - pfsense
---

The newest update for keeping the gaming performance in good shape with pfsense is to put steam-related traffic into lowest priority, or maybe just put it into single WAN.

This can be be done with simple rules. The same rules can be used for tagging the traffic, and prioritizing them down in the QoS side (or we could even put a a network limitter for steam traffic).

<figure class="wp-block-image size-large">![](/wp-content/uploads/2021/11/pfsense_network-1024x322.png)<figcaption>the steamcache is separated from rest of the network with source and destination rules</figcaption></figure>
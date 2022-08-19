---
layout: post
title: "Pfsense multiwan rules based on odd / even LAN ip"
author: Summeli
description: "Pfsense multiwan routing based on odd / even ip on LAN"
categories:
    - pfSense
tags:
    - pfsense
---

In this case we're having two WAN connections that could be shared to the LAN. Insted of setting weight etc on gatewaygroups we're load balancing the traffic based on the user's IP (odd/even). With this setup it's also easy to debug if someone is having a bad Internet connection. 

## Setting aliases for odd and even IPs

## Routing based on the ips

## Extra alias for servers
We're also having some game servers which might need to download updates etc. from the Internet. These are routed through the same WAN as steam cache, and all content that's beging downloaded from the Internet.
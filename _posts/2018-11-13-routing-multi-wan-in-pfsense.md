---
id: 11741
title: 'Routing multi-WAN in pfSense'
date: '2018-11-13T18:16:48+02:00'
author: Summeli
layout: post
guid: 'https://www.summeli.com/?p=11741'
permalink: /11741/
categories:
    - pfSense
tags:
    - devops
    - gateway
    - lan
    - networking
    - party
    - pfsense
    - routing
---

I just added a third WAN connection into my pfSensebox for LAN parties. However the configuration was pretty tricky and I forgot most of the settings, so I wrote this quick guide to follow for the future (if I have to do it again..)

#### Configure WANs

The fist step is to configure WANs. Just configure DHCP and internetsettings separably to each WAN.

#### Create Routing Gateways

Go to System-&gt;Routing-&gt;Gateway Groups, and add new

![](/wp-content/uploads/2018/11/gateway_groups.png) in Settings I did set Tier 1 for each connection, so all of them will be used. We’ll set the weights for each gateway later…

![et all gateways into Tier 1](/wp-content/uploads/2018/11/gateway_groups_settings-1.png)<figcaption>Set all gateways into Tier 1

#### Setting Weight for each gateway

 go to Settings-&gt;Routing-&gt;Gateways and select a gateway to edit.

![select gateway to set weight](/wp-content/uploads/2018/11/routing_gateways.png) Select a gateway, and click advanced

![set Weight in advanced settings](/wp-content/uploads/2018/11/gateway_weight.png) The Weight should be configured in the way that the best connection has most weight (more traffic goes into that one). I guess that pfsense is using the weighted round robin algoritm for routing. you can see on the wikipedia page how the weight should affect the traffic routing [https://en.wikipedia.org/wiki/Weighted\_round\_robin](https://en.wikipedia.org/wiki/Weighted_round_robin)

#### Configure the LAN-&gt;Gateway Group binding

The Gateway group can be taken into use in Firewall settings. Go into Firewall-&gt;Rules-&gt;LAN

![Click edit for IPv4 settings](/wp-content/uploads/2018/11/multiwan_firewall-2.png) Select advanced in the IPv4 settings. Choose the gateway group that we just made in the 1stStep.

![](/wp-content/uploads/2018/11/multiwan_advanced.png)

### Traffic Shaper

The trafic shaper is very easy to configure with multilan, thanks to the new traffic shaper wizard (under firewall/traffic shaper). It basically contains settings for prioritizing games, and detecting game downloads (steam etc), so we can put downloads into lower priority than games.
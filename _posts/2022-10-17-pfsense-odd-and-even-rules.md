---
layout: post
title: "Pfsense multiwan rules based on odd / even IP"
author: Summeli
description: "Pfsense multiwan routing based on odd / even ip on LAN"
categories:
    - pfSense
tags:
    - pfsense
---

In this case we're having two WAN connections that could be shared to the LAN. Insted of setting weight etc on gatewaygroups we're load balancing the traffic based on the user's IP (odd/even). One of be benefits of this setup is, that it's easy to debug if someone is having a bad Internet connection. 

We're also adding upload / download limits per user to keep both of the connections working for everyone.

## Setting aliases for odd and even IPs

Let's go to Firewall->Aliases and set aliases for both odd, and even LAN ips. Let's add all odd and even ips which are in our dhcp ip range.

![](/img/2022/pfsense_lan_alias.png)

## Routing based on the aliases

Now we can set the routing based on alias. Go to Firewall->Rules, and set routing rules for odd, and even ip's. Note that the lancache has own WAN.

![](/img/2022/pfsense_firewall_odd_even_rules.png)

## Addling lmitters to FW rules

Select Firewall/Traffic Shaper and Limitters.

Create network limitters for upload and download
![](/img/2022/pfsense_limitupload.png)
![](/img/2022/pfsense_limitdownload.png)

Then go to Firewall / Rules. Select a rule, and click advanced
add upload and download rules to in / out pipes

![](/img/2022/pfsense_rule_limitter.png)

## Results 

Writing static routes to pfSense seems to be working a lot better than any load balancing strategy. 
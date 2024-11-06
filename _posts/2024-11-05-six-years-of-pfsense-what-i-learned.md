---
layout: post
title: "6 years with pfsense: What I have learned"
author: Summeli
description: "I have been running pfsense and lancache (or steamcache) six years. Here's what I have learned so far"
categories:
    - pfsense
tags:
    - pfsense
    - lancache
    - lanparty
---
We've been hosting LAN parties for 18 years now. When we started, nearly every online game offered a LAN option. Today, however, LAN functionality is much rarer, and we typically rely on online servers. Despite this shift, it's still possible to have a great time with friends in the same location—the spirit of LAN gaming is alive and well. All we need is a good internet connection to play games online.

## Network Setup
We typically host around 30-40 people at our LAN parties. Setting up the network is straightforward. Our early setups were more experimental, but over time, we've refined the process.

Initially, we used three 4G internet connections, pfSense for multi-WAN management, and LanCache (originally SteamCache) to cache games.

## Lessons learn from loadbalancing multi-WAN connections
Load balancing with multiple WAN connections turned out to be more complicated than we expected. One major issue was that TCP connections tend to stay on the same WAN once they've been established. This became problematic because we were using three different network operators, and if one connection was slow or unreliable, all the traffic on that WAN would suffer.

It took a few iterations to identify the best operator, and eventually, we consolidated all our connections under the top-performing provider. We found that it was far better to have three solid 4G connections from the same ISP than to rely on three different ISPs with varying performance.

The debugging process became much smoother once we implemented our static rules. You can read more about this in our previous post: [Odd and Even Rules with pfSense ]({% post_url 2022-10-17-pfsense-odd-and-even-rules %})

## 5G is a Game Changer
Just as we were getting our multi-WAN setup working well, we got access to 5G connections. The difference in latency between 5G and 4G is incredible—it's literally night and day. At that point, I designated one 4G connection for LANCache to download games and content, while the rest of the LAN party used the 5G connection.

One 5G connection was more than enough to provide a stable internet connection and low latency for all online games. To ensure good performance, we limited the bandwidth to about 5 Mbps per user, which was sufficient to guarantee good ping times to the game servers.

5G has been amazing here in Finland!

![](/img/2024/2024-04-5g-rules.png)

## Our New Place: 1 Gigabit Internet
We recently found a new venue for our LAN parties, and it's equipped with 1 Gigabit internet, powered by Ubiquiti airFiber. With this setup, we no longer need multi-WAN configurations and have connected everything through this single, high-speed connection.

LANCache is essentially running on unlimited bandwidth, and we've set user bandwidth limits to 50 Mbps, which provides more than enough speed for gaming. At this point, there's not much to blog about in terms of pfSense configurations—everything is much simpler with a fast and reliable internet connection.

Here's a picture of our pfSense box with a single WAN connection:
![](/img/2024/2024-11-singlewan.jpg)

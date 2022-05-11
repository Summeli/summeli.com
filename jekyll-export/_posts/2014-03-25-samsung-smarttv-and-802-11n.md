---
id: 5056
title: 'Samsung SmartTV and 802.11n'
date: '2014-03-25T17:37:31+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=5056'
permalink: /5056/
categories:
    - Tips
tags:
    - cisco
    - crap
    - E4500
    - GreenField
    - linksys
    - rant
    - Samsung
    - smarttv
    - wifi
---

I just bough a new Samsung SmartTV (model UE46F6400). I just spent few hours just to configure the Wlan connection on it correctly. The TV can connect into the WLAN, but it disconnects after about 30 seconds, and then you’ll have to re-enter the password etc. to get it connected again for about 30 seconds, before it disconnects again.  
I used the Ethernet connection to update the device firmware, but it did not help. I got multiple hits just by Googling the issue about Samsung SmartTVs that are disconnecting from the network. One blogger seemed to have similar problem as did I: <http://blog.alexanderwinkler.se/post/53743100177/samsung-smart-tv-and-cisco-linksys-router> However setting the WPA2 down to the WPA also downgrades the wifi n spec into lower bandwidth. I even tested this with my Cisco Liksys E4500 with both 5Ghz antenna, and 2.4Ghz antenna. The Samsung TV actually can use the WPA2, if the network connection has been set into lower speed.  
Here’s what I got working;

- 5Ghz, Wifi A-connection, not mixed, or N
- 2.4Ghz, B/G Connection, not mixed, or N

After that I had debugged the working Wifi settings I took a quick look at the manual. It says that Samsung recommends 802.11n, and soon after that it says that it doesn’t work correctly with GreenField mode. Yes, I can verify! it does not work. WTF Samsung!  
The thing that troubles me is that the crappy Samsung TV software can not filter the Wlan hotspots that it can not support properly. It’s really frustrating to connect into these networks just to get disconnected after about 30 seconds. I would also like to know why does Samsung recommend using 802.11n in the user manual, while it does not support the specification properly. I bet that the average TV user does not know the difference between 802.11n legacy mode, and the GreenField mode.
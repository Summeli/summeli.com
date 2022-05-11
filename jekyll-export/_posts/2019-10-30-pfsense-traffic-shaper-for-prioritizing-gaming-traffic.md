---
id: 13446
title: 'pfSense Traffic Shaper for prioritizing gaming traffic'
date: '2019-10-30T10:49:36+02:00'
author: Summeli
layout: post
guid: 'https://www.summeli.com/?p=13446'
permalink: /13446/
categories:
    - pfSense
tags:
    - gaming
    - pfsense
    - qos
    - 'traffic shaper'
---

This a lot easier, than I originally though it would be. Works really well on my multiWAN setup too! I did everything with the Wizard, that can be found under firewall/traffic shaper.

### The Wizard

Why even post steps about a traffic shaper wizard? Well, it’s pretty easy to use, so maybe there’s no point. However I tend to forget easy things, like choosing the correct wizard ([traffic\_shaper\_wizard\_multi\_all.xml](https://192.168.0.1/wizard.php?xml=traffic_shaper_wizard_multi_all.xml)), and using high enough connection speed (the first image). Everything else is really simple.  
At the first step we just add the upload / download speed limits. You should use some value that is actually pretty close to the maximum value, since the penaltyBox feature in the next still will only accept persentage of the connection speed, which will be calculated from these values.  
[![](/wp-content/uploads/2019/04/trafic_shaper1-1.png)](https://www.summeli.com/?attachment_id=13461)  
The Scheduler PRIQ means that each packed is placed on separate queue, and the prioritized packets (games) will pass through first.

### Penalty Box

In the next step we can add a penaltybox to drop traffic from certain PCs. In a LAN party we might have someone who is draining a lot more bandwidth than everyone else would accept. In this case we can just put that user (IP) into the penaltybox to stop him draining our bandwidth. I used firewall alias penaltyBox for this purpose. The alias penaltyBox can be edited under Firewall/Aliases.  
[![](/wp-content/uploads/2019/04/trafic_shaper_penaltybox.png)](https://www.summeli.com/?attachment_id=13449)

### Prioritize gaming traffic

After this the wizard is pretty straightforward: just prioritize gaming traffic, and put HTTP, and P2P traffic into lower priority.

### [![](/wp-content/uploads/2019/04/trafic_shaper3.png)](https://www.summeli.com/?attachment_id=13450)

### Finding the worst offender to the penalty box

You can see the realtime data in the Status / Traffic Graph menu. If you’re seeing someone downloading too much, and the rules won’t bite well enough, then you could also add these ips into the penalty box.  
[![](/wp-content/uploads/2019/04/status_graphs.png)](https://www.summeli.com/?attachment_id=13464)
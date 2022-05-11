---
id: 2931
title: 'Solving the 3007 error in Diablo III'
date: '2012-05-24T23:13:05+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2931'
permalink: /2931/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - TCP/IP
tags:
    - 'diablo III'
    - SOCKS5
    - ssh
---

I had pretty much same problem that’s described in this battle.net forum post: <https://eu.battle.net/d3/en/forum/topic/4210083858> Most of the 3007 error pages are just full of trolling, but this one seems quite informative, so I keep that as a reference.  
At fist I started the [WireShark](http://www.wireshark.org/) to see what’s going on. The log was full of TCP Retransmission packets telling me that the TCP packest aren’t going though. My best guess is that my ISP is marking those packets as bittorrent packages, and then the QOS is heavily limiten their bandwidth.  
I filtered the dns records, and I noticed that in the login phase the Diablo III is connecting into eu.actual.battle.net port 1119, and that my network traffic into that IP is quite limited. My first ideas was to create SSH tunnel, and tunnel the port 1119 into the battlenet.

### Creating the SSH tunnel

I added the line to the windows host file, to route all traffic to eu.actual.battle.net into my localhost.

```
<pre class="brush: plain; title: ; notranslate" title="">
#battle.net
127.0.0.1 eu.actual.battle.net
```

After this I opened putty, and set the Tunnel in the Putty’s tunnels menu. I created a local tunnel into port 1119(that’s where I’ll be getting the packages from diablo III), and then I set the destination into eu.actual.battle.net:1119 (where all that data should go).

### Did it work?

Well, it didn’t work. After going though the Wireshark logs I noticed that there are some other ports (seemed like random) opened into eu.actual.battle.net too, and there was some UPD packages as well, so regular SSH tunneling wasn’t enough.  
However in this kinds of situations we can use the [SOCKS5 Proxy](http://en.wikipedia.org/wiki/SOCKS) to tunnel though a single SSH tunnel into the Battle.net

### Creating a SOCKS5 Proxy for Diablo

SOCKS5 to the rescue. I used putty to create the SOCKS tunnel in the Putty’s tunnel menu by biding a local port 9999, and choosing the tunnel type as dynamic. Then I used [Widecap](http://www.widecap.com/) as a proxyfier to make a proxy for Diablo III. I proxied only the IP for the eu.actual.battle.net, since I didn’t wan to was any more bandwidth from my SSH server than I had to. I also blogged about SOCKS5 for Diablo III in more details at <http://www.summeli.com/?p=2933>
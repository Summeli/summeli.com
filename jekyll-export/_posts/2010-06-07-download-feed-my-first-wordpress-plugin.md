---
id: 1769
title: 'Download-Feed: my first WordPress plugin'
date: '2010-06-07T20:08:37+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1769'
permalink: /1769/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - WordPress
tags:
    - download-feed
    - wordpress
---

Download-Feed is a plugin for creating a XML feed from downloads created with [Download-Monitor](http://wordpress.org/extend/plugins/download-monitor/) WordPress plugin.  
The XML feed could be used for integrating a mobile client into the download-interface, so any WordPress powered blog could be turn into “appstore” type of application delivery system, without payments.  
Here’s an example of a donwload entry from the XML-feed.

```
<entry>
    <title>AntSnes_v071.sis</title>
    <version>0.71</version>
    <description></description>
    <category>
      <title>AntSnes</title>
      <ID>1</ID>
    </category>
    <hits>6784</hits>
    <thumbnail>http://www.summeli.com/wp-content/plugins/download-monitor/img/download.gif</thumbnail>
    <link href="<a href="view-source:http://www.summeli.com/wp-content/plugins/download-monitor/download.php?id=5">http://www.summeli.com/wp-content/plugins/download-monitor/download.php?id=5</a>"/>
  </entry>
```

The Downloads can be queried by category, and there’s an option to limit how many items should be requested, and what’s the offset. So it could be used even with very big list of entries (like appstore :))  
  
The feed.php uses following url-parameters  
n: an integer value of how many entries should be queried  
i: an iteger and will offset the returned entries by that number. e.g. offset of 1 would not return the first entry  
cat: category id, which should be returned.  
here’s an example request:

```
http://www.summeli.com/wp-content/plugins/downloadfeed/feed.php?i=2&n=3&cat=1
```

As usual, this plugin is open source, and it can be downloaded from my github page [github.com/Summeli/download-feed](https://github.com/Summeli/Download-Feed)
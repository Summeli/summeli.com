---
id: 4594
title: 'Porting JamendoFM to Tizen'
date: '2013-11-08T16:14:32+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=4594'
permalink: /4594/
categories:
    - 'Web Development'
tags:
    - html5
    - JamendoFM
    - tizen
---

At First I created a new jQueryMobile based UI with Tizen SDK. then I simply addecd the source-code from my JamendoFM project into the Tizen project, and voilà, I got JamendoFM running on Tizen Emulator.  

**The method above got the application running only on Tizen emulator. Running it on the device itself requires correct access policies to the manifest file.**

### Access Policy in Tizen

To get the JamendoFM running on the real device I had to add the urls that JamendoFM uses into the [app manifest file](http://wiki.tizen.org/wiki/Security/Application_installation_and_Manifest). The url can be added like this:

```
<access origin="http://jamendo.com" subdomains="true">
<access origin="http://radionomy.com" subdomains="true">
<access origin="http://imgjam.com" subdomains="true">
```

### Getting the app approved to the Tizen Store

The Tizen QA noticed the there currently are some bugs related to the page-transition effects (it’s not a surprise), so I had to remove those.  
I had places the transition effects into the radioList items, so I had to remove them.  
I also had to make a new circular icon that matches the Tizen design style to get the application approved. The submitting process to Tizen store was pretty fast. I usually got responses from the QA team at the same day when I submitted my application.
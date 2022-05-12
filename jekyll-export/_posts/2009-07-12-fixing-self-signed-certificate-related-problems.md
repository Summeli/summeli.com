---
id: 932
title: 'Fixing self-signed certificate related problems'
date: '2009-07-12T20:31:04+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=932'
permalink: /932/
syntaxhighlighter_encoded:
    - '1'
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - AntSnes
    - S60
---

Currently there isn’t any freeware signing process in the Symbian signed, and I really don’t want to pay for the signing process, so that leaves only self-signing for me. The AntSnes is signed with self-signed certificate, so the user must grant the capabilities for the application (it requires none). This should all work very well with the standard installation process. The installer will ask if user allows the application to be installed etc.  
However sometimes there might be issues with the certificate. Then the installer will give you errors like “can not install”, or “certificate error” etc. One possibility is that your phone’s clock is set on wrong time. If the current time is less than the time was when the certificate was created, then the installer can not install the application, since the certificate does not make any sense.  

### Fixing the time 
Go to settings -&gt;General Settings -&gt;Date And Time settings and then set the current time right. See the images below. The menu structure is from N96, so it might be a little different in you phone.  

### Online certificate check
Another common problem seems to be that you have “Online certificate check” in use. The online cerificate check will only accept symbian signed certificates, which I don want to pay for. To install AntSnes or any other apps with self-signed certificate (usually freeware) you must turn it off. Go to Settings -&gt; Applications -&gt; App Manager -&gt; Online certificate check -&gt; Off. See the images below.  

#### online certificate check
![Settings](/jekyll-export/wp-content/uploads/2009/07/settings_apps-150x150.jpg)
![Applications](/jekyll-export/wp-content/uploads/2009/07/app_manager-150x150.jpg)
![App Manager](/jekyll-export/wp-content/uploads/2009/07/onlinecertificatecheck-150x150.jpg)

#### date and time
![Settings](/jekyll-export/wp-content/uploads/2009/07/settings_general-150x150.jpg)
![General Settings](/jekyll-export/wp-content/uploads/2009/07/general_datetime-150x150.jpg)
![Date And Time](/jekyll-export/wp-content/uploads/2009/07/datetime-150x150.jpg)

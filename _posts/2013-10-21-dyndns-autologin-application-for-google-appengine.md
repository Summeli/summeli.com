---
id: 4708
title: 'DynDns Autologin Application for Google AppEngine'
date: '2013-10-21T18:21:26+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=4708'
permalink: /4708/
categories:
    - 'Dev Talk'
    - 'Google Appengine'
    - 'Web Apps'
tags:
    - appengine
---

DynDns recently changed their service so you’ll have to log in once in every 30 days to keep your account active. As it happens I also have had the DynDns package for years, and the new login requirement really bugs me.  
So I developed this simple autologin application for Google’s Appengine to keep my account active. You can download the dyndns autologin app from my GitHub repository at: <https://github.com/Summeli/dyndns-autologin>  
Please notice that this probably violates the DynDns ToS, so you might get your account banned. I will not take the responsibility for that.

### Installation

- Change the application in app.yaml into your own app-id
- Change username and password into the Settings class in cron.py file
- the script automatically executes every Monday
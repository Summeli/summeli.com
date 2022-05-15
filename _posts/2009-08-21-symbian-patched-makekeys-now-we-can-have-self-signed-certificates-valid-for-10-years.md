---
id: 1109
title: 'Symbian patched Makekeys, now we can have self-signed certificates valid for 10 years'
date: '2009-08-21T16:17:35+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1109'
permalink: /1109/
aktt_notify_twitter:
    - 'yes'
syntaxhighlighter_encoded:
    - '1'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - makekeys
---

I don’t know how this got past me. Luckily I found out that Symbian has patched the makekeys.exe. The new one allows you to create self-signed certificates which can be valid for 10 years. I know that there are a lot of people like me whe are still using the old S60 3.0 MR SDK for maximium compability, which gives you certificates valid for only one year. This reminders me that the AntSnes certificate will end up soon, so I should at least sign it with the newer certificate.  
You should get the newer makekeys tool with new Symbian SDK’s. However, I didn’t get newer one with S60 3rd edition FP1 even when it should be using Symbian 9.2. So I guess that Nokia forgot to patch this tool into their SDK.  
If you didn’t get the new makekeys.exe from you new SDK you can download it from [Symbian website.](http://www3.symbian.com/faq.nsf/0/0A641D4666011F9C002572250023F01C?OpenDocument) Enjoy!  
Using the new makekeys.exe:   
```
makekeys -cert \[**-expdays |cert-expiry-in-days|**\]\[-password |password|\] \[-len \[key-length|\] -dname |distinguised-name-string| |priv  
ate-key-file| |public-key-cert|  
```

Notes:  
For -cert if the private-key-file does not exist it will be created  
Distinguished name string format:  
CN – Common Name, e.g. CN=Joe Bloggs  
CO – Country, e.g. CO=GB  
OR – Organisation, e.g. OR=Acme Ltd  
OU – Organisational Unit, e.g. OU=Development  
EM – E-Mail address, e.g. EM=noone@nowhere.com  
A distinguished name strings needs at least two attributes  
Certificate expiry date(in days) can be specified by the user (optional) , else defaults to a year.  
Example Usage for creating a certificate valid for 10 years:  
makekeys -cert -expdays 3650 -password yourpassword -len 2048 -dname “CN=Joe Bloggs OU=Development OR=Acme Ltd CO=GB EM=noone@nowhere.com” mykey.key mycert.cer  
Now you don’t have to sign you app again each year!
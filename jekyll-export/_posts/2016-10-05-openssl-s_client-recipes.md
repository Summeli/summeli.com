---
id: 11162
title: 'OpenSSL s_client recipes'
date: '2016-10-05T14:04:51+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.com/?p=11162'
permalink: /11162/
categories:
    - TCP/IP
tags:
    - certificate
    - openssl
    - s_client
---

This post is pretty much a reminder note to myself how to quickly start debugging certificate errors. I have googled this stuff way too often.  
Checking the certification expiration date:

```
<pre class="brush: plain; title: ; notranslate" title="">
openssl s_client -connect www.google.com:443 | openssl x509 -text
```

You could also add -servername parameter to support new ssl spec

```
<pre class="brush: plain; title: ; notranslate" title=""> openssl s_client -servername google.com -connect www.google.com:443 | openssl x509 -text 
```

Then see these blocks

Validity  
Not Before: Mar 22 00:00:00 2016 GMT  
Not After : Mar 23 23:59:59 2017 GMT

Let’s verify the whole certificate chain:

```
<pre class="brush: plain; title: ; notranslate" title="">
openssl s_client -showcerts -connect www.google.com:443
```

This is the most common case for me. Most of the time the certificate is somehow installed in a wrong way. One common error is that the certificates are sent to the client in wrong order. This is fine for most of the clients, but at least Android seems to be expecting correct certificate order, as specified in the RFC document.  
After this we can make simple GET request to the host with

```
<pre class="brush: plain; title: ; notranslate" title="">
GET /myresource.html HTTP/1.1
Host: www.google.com
```

After this remember to press the enter twice.
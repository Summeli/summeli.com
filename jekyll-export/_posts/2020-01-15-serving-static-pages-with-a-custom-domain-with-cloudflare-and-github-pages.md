---
id: 14648
title: 'Serving static pages with a custom domain with Cloudflare and github pages'
date: '2020-01-15T14:32:51+02:00'
author: Summeli
layout: post
guid: 'https://www.summeli.com/?p=14648'
permalink: /14648/
categories:
    - 'Web Development'
tags:
    - cloudflare
    - github
    - html
---

The idea is pretty cool. You can serve static web-pages for free with your own domain with Cloudflare and Github Pages. The Cloudflare is handling the DNS, page caching, and the TSL certificate. The the pages itself are hosted by github. Here’s a quick tutorial how to do it.

### Cloudflare

Set the DNS to point into Github Pages (<https://help.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site>)

```
<pre class="brush: cpp; title: ; notranslate" title="">
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

## Github

I basically made simple html pages without jekyll.  
First add the CNAME file into the root of your github project for your own domain:

```
<pre class="brush: cpp; title: ; notranslate" title="">
www.finice2020.com
```

After the initial commit I noticed that my images are not found from the server. It turns out that you have to add an empty file named as “.nojekyll” to bypass the jekyll, so the github will know to publish everything under your domain.  
See my example project at:[ https://github.com/Summeli/finice2020.github.io](https://github.com/Summeli/finice2020.github.io)

## MailGun

You can also get free email routes from mailgun. Setting the account for that is also quite simple. Just follow the mailgun tutorial, for dns etc.  
One of the benefits is that you can create rules for forwarding emails like info@mydomain.com and forward those emails for everyone involved in “info”.  
Mailgun no longer supports the email routing for free plans, so I moved into forwardmail.net

## Forwardmail.net

<https://forwardemail.net/> is a much easier service. Just write the forwarding rules into the dns records and you’re good to go. Even better service than mailgun!
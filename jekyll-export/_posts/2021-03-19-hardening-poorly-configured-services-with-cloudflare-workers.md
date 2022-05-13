---
id: 14722
title: 'Hardening poorly configured services with Cloudflare workers'
date: '2021-03-19T10:18:57+02:00'
author: Summeli
layout: post
guid: 'https://summeli.com/?p=14722'
permalink: /14722/
categories:
    - Azure
    - Cloud
tags:
    - asp.net
    - azure
    - cloudflare
    - php
---

It seems that Azure is sending x-powered-by header from asp.net, and also the php version. Removing the asp.net header is easy with web.config changes, but the php is tricker. I decided to remove these unwanted header with cloudflare worker-script.

Here’s a simple workes which will remove the x-powered-by headers from your responses.

<div class="wp-block-syntaxhighlighter-code ">```
<pre class="brush: plain; title: ; notranslate" title="">
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

/**
 * Respond to the request
 * @param {Request} request
 */
async function handleRequest(request) {
  const response = await fetch(request),
  newheaders = new Headers(response.headers);
  newheaders.delete("x-powered-by");

 return new Response(response.body , {
		status: response.status,
		statusText: response.statusText,
		headers: newheaders
	})
}
```

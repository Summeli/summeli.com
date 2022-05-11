---
id: 6286
title: 'Viskisieppo Chrome plugin to bypass glenmorangie.com site restriction to Finland'
date: '2014-10-14T12:30:12+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=6286'
permalink: /6286/
categories:
    - 'Web Apps'
    - 'Web Development'
---

Finnish alcohol politics are like DRM. It has no effective on the abusive users, but it pisses off everyone else. Currently it seems that Whisky site glenmorangie.com is blocking Finnish users due to Finland’s alcohol laws.  
Information want’s to be free, so I made a simple plugin for Chrome to bypass the country block at glenmoorangie.com.

### Download

You can download the plugin from Chrome marketplace: <https://chrome.google.com/webstore/detail/viskisieppo/dgmcbnhfgeejfapefklhjpilfiholhcc?hl=fi>

### How it works

You can download the whole project from my github page: <https://github.com/Summeli/Viskisieppo>  
The plugin basically add, or edits the “X-Forwarded-for” HTTP-headers to make the requests look like they are not coming from Finland. This is basically implemented with Chrome webrequest-API

```
<pre class="brush: jscript; title: ; notranslate" title="">
var requestFilter = {
	urls: [
		"*://*/*"
	]
};
chrome.webRequest.onBeforeSendHeaders.addListener(function(details) {
	var headers = details.requestHeaders;
	var header_set = false;
	for(var i = 0, l = headers.length; i < l; ++i) {
		if( headers[i].name == "X-Forwarded-for" ) {
			headers[i].value = "12.13.14.15";
			header_set = true;
			break;
		}
	}
	if(!header_set){
		headers.push({name:"X-Forwarded-for",value:"12.13.14.15"});
	}
	return {requestHeaders: headers};
}, requestFilter, ['requestHeaders','blocking']);
```
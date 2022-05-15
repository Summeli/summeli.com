---
id: 14726
title: 'Preventing your site from idling out with Cloudflare workers'
date: '2021-04-06T12:41:51+03:00'
author: Summeli
layout: post
guid: 'https://summeli.com/?p=14726'
permalink: /14726/
categories:
    - Azure
    - Cloud
tags:
    - azure
    - cloudflare
---

Azure might just put your app into idle state if it’s inactive for too long. The always on feature is available only for higher app plans.

![](/wp-content/uploads/2021/03/basic_config.png)

However, the same functionality can be achieved by just making http calls with cloudflare workers.

Let’s just create a simple listener:

```
addEventListener("scheduled", event => {
  event.waitUntil(handleScheduled(event))
})

async function handleScheduled(event) {
  await fetch("https://summeli.com")
}
```

And then we just add a cron trigger to launch fetch request every 30 minutes.

[](/wp-content/uploads/2021/03/cron_trigger-1024x239.png)
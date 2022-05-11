---
id: 14674
title: 'Configuring Mime types for Azure and WordPress'
date: '2021-03-16T19:12:39+02:00'
author: Summeli
layout: post
guid: 'https://summeli.com/?p=14674'
permalink: /14674/
categories:
    - Azure
    - Cloud
    - 'Dev Talk'
tags:
    - azure
    - cloud
    - wordpress
---

My blog has been not working so well for quite some time. The Symbian sis file downloads were broken due to broken theme and plugins. After I got the blog working again I wanted to move it into cloud.

I chose Azure, since I haven’t been using that before.

### Configuring MIME types in Azure

First we must teach Azure about Symbian installer files, and debian packages. Go to your App Service in Azure Portal, and look for App Service Editor (Preview). Then we can edit web.config and add the new MIME types to the Azure.

<figure class="wp-block-image size-large">![](/wp-content/uploads/2021/03/web_config.png)</figure>### MIME Types in WordPress

Then it’s time to set MIME types right in WordPress. I did this by installing the **WP Extra File Types** Plugin. And I added the file types in there.

..And now the jorney contines in Azure.
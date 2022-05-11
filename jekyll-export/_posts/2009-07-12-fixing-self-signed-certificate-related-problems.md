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
**Fixing the time**  
Go to settings -&gt;General Settings -&gt;Date And Time settings and then set the current time right. See the images below. The menu structure is from N96, so it might be a little different in you phone.  
**Online certificate check**  
Another common problem seems to be that you have “Online certificate check” in use. The online cerificate check will only accept symbian signed certificates, which I don want to pay for. To install AntSnes or any other apps with self-signed certificate (usually freeware) you must turn it off. Go to Settings -&gt; Applications -&gt; App Manager -&gt; Online certificate check -&gt; Off. See the images below.  
 <style type="text/css">
			#gallery-1 {
				margin: auto;
			}
			#gallery-1 .gallery-item {
				float: left;
				margin-top: 10px;
				text-align: center;
				width: 33%;
			}
			#gallery-1 img {
				border: 2px solid #cfcfcf;
			}
			#gallery-1 .gallery-caption {
				margin-left: 0;
			}
			/* see gallery_shortcode() in wp-includes/media.php */
		</style>

<div class="gallery galleryid-932 gallery-columns-3 gallery-size-thumbnail" id="gallery-1"><dl class="gallery-item"> <dt class="gallery-icon portrait"> [![](/wp-content/uploads/2009/07/onlinecertificatecheck-150x150.jpg)](/wp-content/uploads/2009/07/onlinecertificatecheck.jpg) </dt> <dd class="wp-caption-text gallery-caption" id="gallery-1-941"> App Manager </dd></dl><dl class="gallery-item"> <dt class="gallery-icon portrait"> [![](/wp-content/uploads/2009/07/app_manager-150x150.jpg)](/wp-content/uploads/2009/07/app_manager.jpg) </dt> <dd class="wp-caption-text gallery-caption" id="gallery-1-943"> Applications </dd></dl><dl class="gallery-item"> <dt class="gallery-icon portrait"> [![](/wp-content/uploads/2009/07/settings_apps-150x150.jpg)](/wp-content/uploads/2009/07/settings_apps.jpg) </dt> <dd class="wp-caption-text gallery-caption" id="gallery-1-942"> Settings </dd></dl>  
<dl class="gallery-item"> <dt class="gallery-icon portrait"> [![](/wp-content/uploads/2009/07/datetime-150x150.jpg)](/wp-content/uploads/2009/07/datetime.jpg) </dt> <dd class="wp-caption-text gallery-caption" id="gallery-1-935"> Date And Time </dd></dl><dl class="gallery-item"> <dt class="gallery-icon portrait"> [![](/wp-content/uploads/2009/07/general_datetime-150x150.jpg)](/wp-content/uploads/2009/07/general_datetime.jpg) </dt> <dd class="wp-caption-text gallery-caption" id="gallery-1-936"> General Settings </dd></dl><dl class="gallery-item"> <dt class="gallery-icon portrait"> [![](/wp-content/uploads/2009/07/settings_general-150x150.jpg)](/wp-content/uploads/2009/07/settings_general.jpg) </dt> <dd class="wp-caption-text gallery-caption" id="gallery-1-937"> Settings </dd></dl>  
 </div>
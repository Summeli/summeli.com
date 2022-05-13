---
id: 4355
title: 'Using the same users in SMF Forum and WordPress'
date: '2013-03-20T08:32:23+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=4355'
permalink: /4355/
categories:
    - WordPress
tags:
    - SMF
    - wordpress
---

Lately I have developed our climbing club’s website. My goal was to use the same users in Simple Machines Forum (SMF) and WordPress, so no one would have to remember multiple passwords for one site.  

For the SMF to WordPress integration I strongly recommend smf2wp plugin <https://github.com/jwall149/smf2wp>. It creates new WordPress users for every SMF user who goes to the WordPress site while logged into the SMF. Now the WordPress admin can add access rights to the selected users, so they can add and edit content in WordPress site too!  

We also had some custom pages for certain SMF user groups which shouldn’t be visible for basic users, so we needed a method to check the SMF groups in the WordPress side. That feature didn’t exist in the smf2wp plugin, so I committed a small update to the smf2wp plugin to get the SMF user group check working on the WordPress side.  

Here’s an example how to do the access rights check (currently works only with the latest git-version)

```
global $smf_user_info;
/*The SMF groups that can access the content*/
$accessRights = array(1,2,3);
foreach ($smf_user_info['smf_groups'] as $i =----> $v) {
	$user_groups[$i] = (int) $v;
}
if(array_intersect($user_groups,$accessRights)) {
	echo "<a href="secret_pages">Secret pages for groups 1,2 and 3</a>";
}
```
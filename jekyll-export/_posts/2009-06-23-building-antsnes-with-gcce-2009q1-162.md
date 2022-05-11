---
id: 870
title: 'Building AntSnes with GCCE  2009Q1-162'
date: '2009-06-23T17:34:19+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=870'
permalink: /870/
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
    - GCCE
---

I have been waiting for new GCCE patch from Nokia for ages. The old GCCE is based on GCC 3.4.3, which was originally published in November 2004. Forum.Nokia has a very good article how to hack your Symbian SDK to [support newer GCCE versions.](http://wiki.forum.nokia.com/index.php/How_to_use_GCCE_4_with_Symbian_SDKs) I have been testing the older version from 2008, but none of them really could build AntSnes. However the newest version can! It seems that codesourcer is going into right direction. I had to make some minor changes to the AntSnes code, but it seems to be working quite well.  
One modification was for switch case statements. The GCCE 2009Q1 – 162 seems to be more firm about switch case statements. For example following code isn’t allowed anymore:

```
<pre class="brush: cpp; title: ; notranslate" title="">
switch (a)
{
case 1:
if(my cond)
{
int i=0;
}
break;
case 2:
//mycase
break;
}
```

The switch case must be written like this:

```
<pre class="brush: cpp; title: ; notranslate" title="">
switch (a)
{
case 1:
{
if(my cond)
{
int i=0;
}
}
break;
case 2:
//mycase
break;
}
```

  
The new compiler doesn’t support -finline-functions optimization flag, so it might produce a bit slower code. However the compiler should have a lot of bugs fixed etc, so it could still be a lot faster.  
Download the[ Sourcery G++ Lite 2009q1-162](http://www.codesourcery.com/sgpp/lite/arm/portal/release822) and try it out! It worked really well for me.  
I was testing the new compiler just fun, so I don’t know if anyone should use this build. If you want to try how much faster the new GCCE is, then you can try it. For all new users I would recomment the current[ AntSnes 0.63 release](http://www.summeli.com/?p=845). However I think that the new GCCE build seems to be a bit faster with N96, so you are welcome to try it. Just don’t ask for bug fixes into this version, since there might be bugs caused by the unsupported compiler.  
AntSnes gcce 2009q1 – 162 build: [AntSnes\_GCCE2009Q1\_build.sis](http://www.summeli.com/wp-content/uploads/2009/06/AntSnes_GCCE2009Q1_build.sis)
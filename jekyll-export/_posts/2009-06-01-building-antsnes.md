---
id: 719
title: 'Building AntSnes'
date: '2009-06-01T13:46:29+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=719'
permalink: /719/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
tags:
    - AntSnes
---

I recently received a question via email how to build AntSnes. I decided to make a blog post about it, if anyone else wants to know. AntSnes build as any other S60 project, so if you are already familiar with S60 development, you already know how to build AntSnes. First you should take a peak at [Forum.Nokia Getting started page.](http://www.forum.nokia.com/I_Want_To/Develop_Mobile_Applications/Get_Started.xhtml) The learning curve for Symbian apps is quite steep, which means that you have to spend quite a lot of time for documentation.  
Required tools:

- [S60 3.0 MR Release](http://www.forum.nokia.com/Tools_Docs_and_Code/Tools/IDEs/Carbide.c++/)
- [Carbide 2.x From Forum.Nokia](http://www.forum.nokia.com/Tools_Docs_and_Code/Tools/IDEs/Carbide.c++/)
- GCCE – you should get a copy of GCCE with 3.0 MR Release. Remember to install it.

After you have installed everything you need, you can start building. You should download the AntSnes sources under the new S60 MR release folder. Remember to set the EPOCROOT variable to point into you existing S60 installation.  
You can build the whole project by running these commands at the AntSnes root directory.

```
<pre class="brush: cpp; title: ; notranslate" title="">
bldmake bldfiles
abld build gcce urel
```
---
id: 4220
title: 'Configuring GCCE 4.6.3 for Symbian with Nokia Qt SDK'
date: '2013-01-04T18:04:50+02:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=4220'
permalink: /4220/
categories:
    - 'Symbian Development'
tags:
    - gcc
    - GCCE
    - Symbian
---

PPSSPP is using the GCCE version 4.6.3 for builds, and I wanted to see if there’s anything that I could do to help, so I ended up setting up the development environment. Here’s short instructions how you can configure the GCCE 4.6.3 for Nokia QT SDK.

#### Download the GCCE 4.6.3

Download the [GCCE 4.6. 3 from Mentor Graphics.](http://www.mentor.com/embedded-software/sourcery-tools/sourcery-codebench/editions/lite-edition/)

#### Add new GCCE version to the Qt Creator

Open QtCreator and choose tools-&gt;options and go to build &amp; run tab. You can add your new GCCE version from there.

<div class="wp-caption alignnone" id="attachment_4224" style="width: 310px">![](/wp-content/uploads/2012/12/qtSDK_build_settings-300x251.png)QtCreator project Build Settings

</div>Next. Open up the project that you are building, and then open the project tab on QtCreator, choose Build &amp; Run, and from the build you can choose the new GCCE 4.6.3.

<div class="wp-caption alignnone" id="attachment_4223" style="width: 310px">![](/wp-content/uploads/2012/12/qtSDK_build_and_Run-300x172.png)QtCreator Build and Run settings

</div>#### Add new GGCE version to the SBS buildsystem

Now the Qt Creator uses Symbian SBS buildsystem with flag gcce4\_6\_3, which is not configured in the sbs-config, so it can not build with it yet. Open file \\QtSDK\\Symbian\\tools\\sbs\\lib\\config\\variants.xml and add following lines:

```
<pre class="brush: xml; title: ; notranslate" title="">
&lt;var name="gcce4_6_3" extends="gcce_base"&gt;
 &lt;env name="SBS_GCCE463BIN" type="toolchainpath" /&gt;
 &lt;set name="GCCEBIN" value="$(SBS_GCCE463BIN)" /&gt;
 &lt;set name="GCCECC" value="$(GCCEBIN)/arm-none-symbianelf-g++$(DOTEXE)" type="tool" versionCommand="$(GCCECC) -dumpversion" versionResult="4.6.3"/&gt;
 &lt;set name="RUNTIME_LIBS_LIST" value="drtaeabi.dso dfpaeabi.dso"/&gt;
 &lt;set name="PLATMACROS.VAR" value="GCCE_4 GCCE_4_6"/&gt;
 &lt;set name="ARMMACROS.VAR" value="__GCCE_4__ __GCCE_4_6__"/&gt;
 &lt;set name="LINKER_GROUP_END_OPTION" value="-Wl,--end-group"/&gt;
 &lt;set name="LINKER_GROUP_START_OPTION" value="-Wl,--start-group"/&gt;
 &lt;set name="LINKER_DEFAULT_LIBS" value="-lsupc++ -lgcc -lgcc_eh"/&gt;
 &lt;/var&gt;

<p>And that’s it. Now you can start building with new GCCE 4.6.3. The new GCCE seems quite buggy thing to me. I have random seq fauls etc. with it, so I can not really advice using it, but it may / may not produce better binary.</p>
```
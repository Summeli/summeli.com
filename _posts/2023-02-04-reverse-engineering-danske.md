---
layout: post
title: "Reverse engineering DanskeBank's mobile app for oss-license violations"
author: Summeli
description: "Reverse engineering DanskeBank's mobile app for oss-license violations"
categories:
    - reverse-engineering
    - Android
tags:
    - DanskeBank
    - Reverse-engineering
    - Android
    - Developement
---

This all started when I opened up the DanskeBank's mobileapp and I wanted to see what kind of opensource software they are using. I saw that they have software with BSD3-Clause, MIT and ICS-lisences. However, those links only led to SPDX-license boilerplate site. They don't list the author's whose software they are using! 

![](/img/2023/danske-sc1.jpg)

![](/img/2023/danske-sc2.jpg)

## Reverse engineering the mobile client

I have never reverse-engineered Android software, but I'm curious about whose software they are using whithout giving the proper credit to the authors. I downloaded Android Studio, and opened APK in there and... voilà. There's a lot of open source software packaged within this 60MB mobile app.

![](/img/2023/danske-oss.png)

It seems that they are using a lot of native code with oss licenses, and a lot more! On the JAVA-side they seem to be using a lot of opensource software as well that is not mentioned in the lisenses section. okhttp, shotcutbadger etc. 

![](/img/2023/danske-oss2.png)

### React native

The most interesting part about Danske's mobile app seems that it's been build with react native. Maybe they should also have read the lisence in react native: [https://github.com/facebook/react-native/blob/main/LICENSE ](https://github.com/facebook/react-native/blob/main/LICENSE )

![](/img/2023/danske-react-native.png)   

### OSS Software in Danske's mobileapp

It's pretty clear that this software is build on top of oss components and you should include the original license as part of the software itself. 

### Software with debug-symbols.

I find it very odd that they have few libraries with debug symbols still on them. You would think that a bank would remove those from production build. 

#### lib-hermes-executor-debug

This one was probably due to the bug in react-native. See [https://github.com/software-mansion/react-native-reanimated/issues/3952](https://github.com/software-mansion/react-native-reanimated/issues/3952). Other than this are probaby due to incompetence. 

## Secrets

It's starting to get boring to just see what OSS is inside the app. Let's see if we can find any secrets. Just be searching the word "secret" you'll find these. 

```
clientSecret
apiConnectXIbmClientId
apiConnectXIbmClientSecret
reactnativepushnotificationsecret
```

You can find the values pretty easiy to all of these. Some of them are obfuscated, but at least prodEnvironmentObfuscationConfig.java is pretty easy to read (that's another story). I wonder if it makes a lot of sense to use IBM api connection product and then create such a shitty app. 

## Connections

Let's see where the client takes connections. It seems that they are making connections to the "apiebank3.danskebank.com"
and they are pinning the Globalsign's root certificate (which is already trusted by platfom). This really doesn't help you that much. If the root is compromized, then your whole app is.

```
new-instance v0, Lokhttp3/CertificatePinner$Builder;
invoke-direct {v0}, Lokhttp3/CertificatePinner$Builder;-><init>()V
const-string v1, "sha256/cGuxAXyFXFkWm61cF4HPWX8S0srS9j0aSqN0k4AP+4A="
filled-new-array {v1}, [Ljava/lang/String;
move-result-object v1
const-string v2, "apiebank3.danskebank.com"
```

![](/img/2023/danske-trust-store.png)

### Crashlogs

It seems that they are sending the program crash logs into https://danskebank.tpa.io. There's no certificate pinning, and that site seems to be accepting connections with TSL 1.0 and 1.1. It's really not following the best practises. Well, those are only crash logs. 

## Decompiling the code

The code could also be decompilet into easily human readable format with jd-gui. I used jd-gui plugin for IntteliJ. It seems that Danske is still using JAVA 6 to compile their sources (bytecode version 50). WTF are they doing? 

## Conclusions

For me it seems that Danske does not care much about their mobile app. It's a big mess. I would like to ask them to update the app to include the open source licenses, but it seems that they have even bigger issues with the development. 
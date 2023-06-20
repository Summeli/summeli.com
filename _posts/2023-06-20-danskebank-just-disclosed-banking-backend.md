---
layout: post
title: "Unveiling the Curtain: Danske Bank's Revelation of Backend Frameworks and Dependencies"
author: Summeli
description: "DanskeBank just disclosed alot of information about their mobile banking backend"
permalink: "posts/danskebank-incident"
categories:
    - reverse-engineering
tags:
    - DanskeBank
---

In my previous post I complained about [DanskeBank's oss licence violations](/post/reverse-engineering-danske/). Their newest version of the mobile app fixes this issue, but it also leaks a lot of information about their mobile banking backend. You can see that they are running the backend with Ruby on Rais on AWS, and what depencendies (with version infromation) they have in the mobile backend.

Disclosing this information was not required, since it's not part of the binary which is deliverd to users via appstore. 

This accidental exposure instantly provided potential attackers with valuable insights into the bank's infrastructure, creating a dangerous scenario for both the bank and its customers.

## The Risks of Exposing Server Backend Dependencies

1. Targeted Exploits:
By openly revealing their server backend dependencies, Danske Bank inadvertently provided a roadmap for attackers to identify potential vulnerabilities and weak points in their system. Armed with this information, malicious actors can specifically tailor their attacks, increasing the likelihood of successfully breaching the bank's security measures.

2. Known Vulnerabilities:
Exposing specific versions of server backend dependencies enables attackers to cross-reference them with publicly known vulnerabilities. Even if the bank promptly patches any identified security flaws, attackers can exploit unpatched systems that might still be in use, posing a significant risk to customer data and the bank's reputation.

3. Increased Attack Surface:
Sharing detailed information about server backend dependencies unnecessarily expands the attack surface. With specific versions and frameworks readily available, potential attackers have a better understanding of the bank's technological infrastructure, increasing the chances of finding exploitable vulnerabilities.

## Best Practices

DanskeBank should create a process how to use Open Source software inside the company, and what information they should disclose to the users.




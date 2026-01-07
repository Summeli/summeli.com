---
layout: post
title: "Hetuveks.fi remove finnish ssn from your pdf documents"
author: Summeli
description: "Hetuveks.fi remove finnish ssn from your pdf documents"
categories:
    - service
tags:
    - hetuveks
---

Over the years, while attending apartment viewings in Oulu, my email inbox has ended up receiving the personal identity codes of what feels like every second person in the city.

In old land-use agreements, rental contracts, and other attachments, personal identity codes are almost always included. In practice, this means my email inbox is full of people’s personal data — a setup that doesn’t really hold up when viewed through the lens of information security, GDPR, or common sense.

During the Christmas holidays, I decided to do something about it and built https://hetuveks.fi.
The service automatically removes personal identity codes from PDF documents.

Hetuveks works with:
	•	text-based PDF files
	•	as well as old scanned documents where identity codes appear as images (OCR support)

Based on my own test data, it works surprisingly well — even with the worst cases, like documents scanned back in the 1990s.

Building the service with today’s AI tools was, honestly, a lot of fun, and things came together quickly. Looking at the finished product now, it has a bit of a honeypot feel to it. Then again, my email inbox is already quite the honeypot as it is.

To be honest, I wouldn’t necessarily upload the most sensitive documents to a random website myself. That’s why this feels like the most natural solution when integrated directly into, for example, a real estate company’s own systems, where these documents are already being handled.

The idea stuck with me. Let’s see where it leads.

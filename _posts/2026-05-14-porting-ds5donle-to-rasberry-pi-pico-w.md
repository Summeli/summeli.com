---
layout: post
title: "Porting DS5Dongle to Raspberry Pi Pico W"
author: Summeli
description: "I ported the DS5Dongle project from Raspberry Pi Pico 2 W to the older Pico W. The process involved lowering clock speeds, disabling DualSense audio processing, and fixing timing issues with the Infineon CYW43439 Bluetooth chip."
categories:
    - dev
    - devtalk
tags:
    - ds5dongle
---
# Porting DS5Dongle to Raspberry Pi Pico W

I recently came across the awesome [DS5Dongle project](https://github.com/awalol/DS5Dongle), which adds proper wireless support for the PlayStation 5 DualSense controller — including adaptive triggers and haptics.

The project officially supports the Raspberry Pi Pico 2 W, but I happened to have an older Raspberry Pi Pico W sitting in my drawer. Since both boards use the same Infineon CYW43439 Bluetooth/Wi-Fi chip, I figured this should be a relatively easy port.

Well… mostly.

## First Attempt: Just Change the Target

I started by taking a quick look at the build configuration and simply changing the target board from Pico 2 W to Pico W.

That did not work.

The board stayed completely silent.

After a bit of digging, I realized the Pico W could not handle the same CPU clock settings as the Pico 2 W build. The original project runs at a much higher clock speed, so I lowered it to 200 MHz for the Pico W.

That immediately brought the board back to life.

## Audio Processing Had to Go

The next challenge was audio processing.

The Pico W has noticeably less performance headroom than the Pico 2 W, and audio support was one of the heavier parts of the project. I decided to introduce a separate build flag that disables DualSense audio processing entirely.

Honestly, I consider this more of a feature than a limitation.

I usually play with headphones when my kids are asleep anyway, and the tiny speaker on the DualSense controller has always felt awkward to me. Losing controller audio was completely acceptable if it meant keeping adaptive triggers and haptics working wirelessly.

## The Bluetooth Chip Mystery

At this point, the Pico W was clearly running code — but Bluetooth was completely dead.

The funny part was that debugging became unexpectedly difficult because the Pico W’s onboard LED is actually controlled through the Infineon CYW43439 chip itself. Since the chip was not functioning properly, even LED blink debugging stopped working.

That made things slightly more entertaining.

Luckily, the fix turned out to be fairly simple: the bus speed divider for the CYW43439 communication interface needed to be lowered. Once I adjusted that, the wireless stack immediately started behaving correctly.

## Success

After a few more tweaks, everything finally came together.

The result is a fully working DS5Dongle build for the Raspberry Pi Pico W, complete with:

- Wireless DualSense support
- Adaptive triggers
- Haptics
- Stable Bluetooth connectivity

And honestly? I do not miss the controller audio at all.

Getting proper adaptive triggers and haptics working wirelessly on PC feels fantastic. This is something Sony really should have supported years ago.

The best part is that this now works on extremely cheap and widely available hardware — even the older Pico W that many people already have lying around.
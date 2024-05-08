---
layout: post
title: "Nvim pluging with Lua: html-entities"
author: Summeli
description: "I wrote a simple nvim plugin with lua"
categories:
    - dev
    - devtalk
tags:
    - nvim
    - lua
    - plenary
---

At work, we have a pretty nice Web UI to generate json for our mobile app. The tool has a one small problem, it sometimes uses html enocding to encode some special charactes. I wanted to have a quick way of decoding these files into walid json, so I wrote a nice plugin for nvim.

The project is reallu simple. See it at: [Github](https://github.com/Summeli/html-entities.nvim) It really just uses an existing lua library by [TiagoDanin](https://github.com/TiagoDanin/htmlEntities-for-lua).

I made a pretty nice github project for nvim plugin development. If you're staring to make a new one, you should really check this one out. It has linting, prettier, tests, document generation etc. on the pipeline. It's also a nice example for very simple Plenary tests. 
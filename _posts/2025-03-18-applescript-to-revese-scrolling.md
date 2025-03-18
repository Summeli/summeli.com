---
layout: post
title: "Applescript to reverse scrolling"
author: Summeli
description: "Applescript to reverse scrolling"
categories:
    - apple
tags:
    - applescript
---

The UnnaturalScrollWheels application stopped working for me. I really need to keep scrolling in unnatural mode while using natural mode with the trackpad.

The next best solution is to create a new shortcut in Apple’s Shortcuts app. Just open the Shortcuts app, add a new shortcut, and select AppleScript.

Here's a script from [stackoverflow](https://stackoverflow.com/questions/30767674/how-to-set-up-a-keyboard-shortcut-on-my-mac-to-change-scroll-direction) that will reverse the scrolling. 

```
on run {input, parameters}
	do shell script "open x-apple.systempreferences:com.apple.Trackpad-Settings.extension"
	delay 1.0
	
	tell application "System Events"
		tell process "System Settings"
			click radio button 2 of tab group 1 of group 1 of group 2 of splitter group 1 of group 1 of window 1
			click checkbox "Natural scrolling" of group 1 of scroll area 1 of group 1 of group 2 of splitter group 1 of group 1 of window 1
			tell application "System Settings" to quit
		end tell
	end tell
	
	return input
end run
```
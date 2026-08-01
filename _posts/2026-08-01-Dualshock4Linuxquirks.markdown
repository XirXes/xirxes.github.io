---
layout: post
title:  "Fixing Dualshock 4 Stutter on Linux."
---


I fixed up my old Dualshock 4 recently, but found I was having severe stutter when trying to use it to play on my ArchLinux desktop, even more surprising considering how well it works in Windows on the same machine. I couldn't find any similar reports online, but I did find a solution. I could see this also helping with similar issues on the Dualsense controller, they share a kernel driver.

When paired over Bluetooth the contoller actually appeared as a mouse in my settings, and indeed the trackpad worked, poorly. Steam and Games also detected the inputs, and would work well for a short time, before it would stutter and lag. Using `evhz` I was able to verify the poll rate dropping as low as 20Hz, unusable. 

The issue it turns out, is some powersaving feature in libinput activating when the touchpad goes unused. I suspect only one of these files is needed to resolve the issue, but I'm not one to solve problems with surgical precision when a hammer is within reach. 

`/etc/libinput/local-overrides.quirks`
```
[DS4 V1 BT Touchpad Fix]
MatchName=Wireless Controller Touchpad
MatchBus=bluetooth
AttrEventCodeDisable=ABS_X;ABS_Y;ABS_MT_POSITION_X;ABS_MT_POSITION_Y
```

`/etc/udev/rules.d/99-ds4-touchpad.rules`
```
ACTION=="add|change", KERNEL=="event*", ATTRS{name}=="*Touchpad", ENV{ID_INPUT_MOUSE}="", ENV{ID_INPUT_TOUCHPAD}="0", ENV{LIBINPUT_IGNORE_DEVICE}="1"
```

---
template: post
title: How I fixed "Battery drain after shutdown" issue in my ThinkPad e560 laptop
slug: /posts/power-drain-after-shutdown
draft: false
priority: 0
date: 2020-08-02T05:32:30.161Z
description: The battery started to drain overnight in my laptop Thinkpad e560
  after switching to Ubuntu from the windows 10. Recently, I was able to fix
  battery drain after shutdown issue.
category: issues
tags:
  - ubuntu
  - shutdown
  - laptop
  - battery
  - power-drain
  - battery-drain
  - lenovo
---
![battery drain even after shutdown](/media/drain.jpg "battery drain even after shutdown")

*Photo Courtesy: Google*

I recently switched to Ubuntu 20.4 LTS and said goodbye to Windows 10. After switching to Ubuntu, I felt the performance of my laptop is better than earlier. Even the battery backup was increased by an hour. However, I started to notice one problem. Every morning when I open my laptop, it used to be dead. Initially, I didn't take it seriously but when it started occurring rapidly, I started investigating it. I tried shutdown from the command line to make sure it has shut down properly.

```shell
shutdown -h now
```

 I closed WiFi and Bluetooth before switching it off. But, the result was same. I then removed the battery and let it out for the night to check whether the issue was with battery or not. Next day when I attached it, the battery was  100% same as what I had left.

I started to search for the solution online. I read lots of posts and forums. I tried various solution. Even, I executed some of the commands without knowing what it actually does. I posted a query in stack overflow and superuser. Some of them gave some solutions but there was no luck. I spent a lot of time to fix it before I gave up.

One day, I thought of changing the version of my Ubuntu from 20.04 to 18.04 in assumptions that there might be some issue with this latest version of Ubuntu. I booted my laptop to the older version but the result was again the same.

Then and there I realized that this issue is not something related to my OS. This could have occurred due to some issue in Bios or firmware. I searched for the solution with the new issue and there I was with the perfect solution after the months.

## What was the solution to Battery drain after shutdown issue?

 I changed two configurations in my Bios Setting which solved my problem.

### Wake-on-LAN

According to Wikipedia, " **Wake-on-LAN**(**WoL**) is an[](https://en.wikipedia.org/wiki/Ethernet "Ethernet") Ethernet or token ring computer networking standard that allows a computer to be turned on or awakened by a network message." I disabled it from my Bios setting.

![wake on LAN](/media/wol.jpg "wake on LAN")

### Always-On USB

The "Always On USB" feature that comes on most of the ThinkPad laptops allow you to charge your mp3 player, phone and gadgets even when your laptop is turned on. I also disabled it from my Bios Setting.

![always on usb](/media/always-on-usb.jpg "always on usb")

That was all. Now, my battery is fresh and awake when I turn my laptop on.  Thanks for reading it :) I hope it might be helpful to you if you are facing a similar issue too.
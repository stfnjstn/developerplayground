---
layout: post
permalink: /how-to-debug-on-a-real-apple-watch/
title: How to debug on a real Apple Watch
seo_title: How to debug on a real Apple Watch
description: 'Debug on a real Apple Watch: Let XCode manage the changes on your provisioning
  profiles and the registration of your watch in the developer portal.'
date: 2015-04-29 21:08:58 -0000
last_modified_at: 2020-05-27 16:40:54 -0000
publish: true
pin: false
categories:
- Apple Watch
- SWIFT
- WatchKit
tags:
- AppleWatch
- WatchKit
---
## Today my Apple Watch was delivered :-)

I immediately tried to deploy my prototypes to the Apple Watch, to see how the behave on real hardware. The simulator gives only a first impression. **Here are my learnings:** Basically you need to perform two steps:

  * Add the UDID of your apple watch to the developer portal
  * Update your provisioning profile to support the watch

Luckily XCode can manage the whole process for you.  First you need a sample project like this from NatashaTheRobot: [WatchKitTableDemo](https://github.com/NatashaTheRobot/WatchKitTableDemo) 

#### 1. Deploy the App to your iPhone/iPad
[![Debug Apple Watch part1](/developerplayground/assets/2015/04/Screen-Shot-2015-04-29-at-22.53.24-1.jpg)](/developerplayground/assets/2015/04/Screen-Shot-2015-04-29-at-22.53.24-1.jpg) 

#### 2. Start the WatchKit App also on your iPhone/iPad (not in the simulator)
[![Debug Apple Watch part2](/developerplayground/assets/2015/04/Screen-Shot-2015-04-29-at-22.55.14-1.jpg)](/developerplayground/assets/2015/04/Screen-Shot-2015-04-29-at-22.55.14-1.jpg)

#### 3. Choose Fix Issue, when this error message appears:
[![WatchKit Error Message](/developerplayground/assets/2015/04/watch1-1.jpg)](/developerplayground/assets/2015/04/watch1-1.jpg) [![Select team from Apple Developer Portal](/developerplayground/assets/2015/04/watch2.png)](/developerplayground/assets/2015/04/watch2.png)

#### 4. Select your Development Team:
[![watch3](/developerplayground/assets/2015/04/watch3.png)](/developerplayground/assets/2015/04/watch3.png "XCode Watch Kit select team")

That's all. After a short time XCode has created and downloaded a new profile and added your Apple Watch to the devices section in the Apple Developer Portal.

Cheers,    
Stefan 

---
layout: post
permalink: /howto-implement-endless-scrolling/
title: 'HowTo: Implement endless scrolling in iOS and ObjectiveC'
seo_title: 'HowTo: Implement endless scrolling'
description: iOS Tutorial, endless scrolling, infinite scrolling, game development,
  objectiveC, ObjectiveC
date: 2014-03-18 07:24:00 -0000
last_modified_at: 2020-05-27 16:40:55 -0000
publish: true
pin: false
categories:
- iOS
- ObjectiveC
- Parallax Effect
- Scrolling
tags: []
---
### Welcome to Part 4 of my blog series about game development: Endless Scrolling

Today I'm showing how to implement an endless scrolling which is typical for Jump & Run games.

First of all you need a background with 3 sections like the one shown below:

[![](/assets/wp-content/uploads/2014/03/Scrolling1.jpg)](/assets/wp-content/uploads/2014/03/Scrolling1.jpg)

Section 1 and 3 must be identical and have to fit on the whole screen.

[![](/assets/wp-content/uploads/2014/03/Scrolling2.jpg)](/assets/wp-content/uploads/2014/03/Scrolling2.jpg)

[![](/assets/wp-content/uploads/2014/03/Scrolling3.jpg)](/assets/wp-content/uploads/2014/03/Scrolling3.jpg)

If you reach the end of the world (section 1) you have to switch back to section 3.

[![](/assets/wp-content/uploads/2014/03/Scrolling4.jpg)](/assets/wp-content/uploads/2014/03/Scrolling4.jpg)

After that you can start scrolling again.

[![](/assets/wp-content/uploads/2014/03/Scrolling5.jpg)](/assets/wp-content/uploads/2014/03/Scrolling5.jpg)

I've created a small video to demonstrate this:
[![Video](/assets/wp-content/uploads/2014/03/Video.png)](https://youtu.be/-FX-tFks5pg)

That's all for today. In my next post I'll show how to implement this in Objective C and I'll add some nice parallax effects. Cheers, Stefan

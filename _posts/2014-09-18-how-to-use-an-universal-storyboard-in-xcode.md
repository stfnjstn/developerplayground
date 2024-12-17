---
layout: post
permalink: /how-to-use-an-universal-storyboard-in-xcode/
title: How to use an Universal Storyboards in Xcode
seo_title: How to use an Universal Storyboards in Xcode
description: How to use an Universal Storyboards in Xcode a nice concept for targeting
  multiple form factors. Topic for todays post of my iOS game development blog
date: 2014-09-18 21:41:00 -0000
last_modified_at: 2020-05-27 16:40:54 -0000
publish: true
pin: false
categories:
- iOS
- ObjectiveC
- Storyboard
- UIKit
- Xcode
tags: []
---
**Welcome to Part 13 of my blog series about iOS game development: Universal Storyboards**

At the developer conference WWDC, in June this year, Apple showed a nice concept for targeting multiple form factors: The Universal Storyboards. Basically this replaces the iPad and the iPhone specific storyboards with one universal storyboard. To enable different layouts for tablet and phone form factors it's working closely together with Autolayout and Size Classes. I'll not explain Autolayout and Size Classes deeply in this post. My main motivation was to find out how to convert an old Xcode project with two storyboards into one universal storyboard. If you start a new project, the universal storyboard will be created by default.

As a start project you can use the MyGame project from my earlier posts. You can download it from GitHub: [v0.9](https://github.com/stfnjstn/MyFirstGame/releases/tag/v0.9)

This sample needs Xcode 6.

### Create an universal storyboard:

1\. Delete one of the the existing storyboards. In this example the iPad version:

[![](/assets/wp-content/uploads/2014/09/Bildschirmfoto-2014-08-10-um-23.43.12.png)](/assets/wp-content/uploads/2014/09/Bildschirmfoto-2014-08-10-um-23.43.12.png)

2\. Rename the iPhone Storyboard:

[![](/assets/wp-content/uploads/2014/09/Bildschirmfoto-2014-08-10-um-23.43.54-1.jpg)](/assets/wp-content/uploads/2014/09/Bildschirmfoto-2014-08-10-um-23.43.54-1.jpg)

3\. Select the new storyboard as Main Interface for iPhone and iPad:

[![](/assets/wp-content/uploads/2014/09/Bildschirmfoto-2014-08-10-um-23.44.29.png)](/assets/wp-content/uploads/2014/09/Bildschirmfoto-2014-08-10-um-23.44.29.png)

4\. Open the storyboard and enable Auto Layout and Size Classes:

[![](/assets/wp-content/uploads/2014/09/Bildschirmfoto-2014-08-10-um-23.47.29.png)](/assets/wp-content/uploads/2014/09/Bildschirmfoto-2014-08-10-um-23.47.29.png)

5\. Confirm to enable size classes:

[![](/assets/wp-content/uploads/2014/09/Bildschirmfoto-2014-08-10-um-23.47.37-1.jpg)](/assets/wp-content/uploads/2014/09/Bildschirmfoto-2014-08-10-um-23.47.37-1.jpg)

That was easy. Now let's test it:

  * iPhone:
[![](/assets/wp-content/uploads/2014/09/Foto-1-1.jpg)](/assets/wp-content/uploads/2014/09/Foto-1-1.jpg)

  * iPad:
[![](/assets/wp-content/uploads/2014/09/IMG_0002_2.jpg)](/assets/wp-content/uploads/2014/09/IMG_0002_2.jpg)

Hmmmh. We must have missed something.

### Adding Auto Layout Constraints and Size Classes:

We have used the iPhone Storyboard as the new main Storyboard, with a per pixel positioning of the views and UI elements. Therefore it's not surprising, that the iPad layout looks weird. 
Let's have a look on the view structure. For all elements we have to specify positions and size independent from the form factor or orientation:

[![](/assets/wp-content/uploads/2014/09/Bildschirmfoto%2B2014-08-14%2Bum%2B00.59.08.png)](/assets/wp-content/uploads/2014/09/Bildschirmfoto%2B2014-08-14%2Bum%2B00.59.08.png)[![usb1](/assets/wp-content/uploads/2014/09/usb1.png)](/assets/wp-content/uploads/2014/09/usb1.png)

To address this I've added several AutoLayout constraints:

[![usb2](/assets/wp-content/uploads/2014/09/usb2-1.jpg)](/assets/wp-content/uploads/2014/09/usb2-1.jpg)

To model a different layout for iPhone and iPad Size Classes can used. Click at the bottom of the Xcode screen to select a special size class (for example for phone landscape). All new constraints will be limited to the chosen Size Class. Be aware that Size Classes are only working on iOS 8 devices.

[![usb3](/assets/wp-content/uploads/2014/09/usb3-1.jpg)](/assets/wp-content/uploads/2014/09/usb3-1.jpg)

Constraints which are limited to a special Size Class are grayed out. The Size Classes are only working on iOS 8 devices.

[![usb4](/assets/wp-content/uploads/2014/09/usb4-1.jpg)](/assets/wp-content/uploads/2014/09/usb4-1.jpg)

If you need further information here are two excellent articles about Auto Layout and Size Classes:

  * [Introduction to Auto Layout](http://www.appcoda.com/introduction-auto-layout/)
  * [Adaptive Layout](http://www.shinobicontrols.com/blog/posts/2014/07/28/ios8-day-by-day-day-7-adaptive-layout-and-uitraitcollection)


### Auto Layout and dynamic view manipulation

OK, let's test it. At a first glance everything looks great, but the parallax effect from the sample project is no longer working. If you think about it, the cause is obvious: I've manipulated the size and the behavior of the UI elements in the ``ViewDidLoad`` method. After executing this method the Autolayout Constrains are evaluated and the manual changes are overridden.

To solve this move the code which manipulates UIViews to the ``viewDidLayoutSubviews`` method:

Remove from ``viewDidLoad``:
```objectivec
[UITools assignBackgroundParallaxBehavior:self.backgroundView];
[UITools assignForegroundParallaxBehavior:self.foregroundViews];
```

Create ``viewDidLayoutSubviews``:

```objectivec
-(void)viewDidLayoutSubviews {
  [super viewDidLayoutSubviews];
  [UITools assignBackgroundParallaxBehavior:self.backgroundView];
  [UITools assignForegroundParallaxBehavior:self.foregroundViews];
}
```

The other screens/view controllers of my sample project must be updated the same way.

That's all for today. You can download the complete code from [GitHub v0.10](https://github.com/stfnjstn/MyFirstGame/releases/tag/v0.10). An updated version to XCode 6.3 can be found [here](https://github.com/stfnjstn/MyFirstGame).

Cheers,   
Stefan

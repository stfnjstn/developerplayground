---
layout: post
permalink: /applewatch-digitalcrown-control-sprite/
title: Apple Watch as a Gaming Platform - Use the Digital Crown to control sprite
  movement for a Pong like game
description: Apple Watch as Gaming Platform. Tutorial about using the Digital Crown
  as Game Controller to control Sprite movement and animation.
date: 2016-04-09 20:36:10 -0000
last_modified_at: 2020-05-27 16:40:53 -0000
publish: true
pin: false
image:
  path: /assets/wp-content/uploads/2016/04/WatchPingPongGif.gif
categories:
- Apple Watch
- WatchKit
tags:
- AppleWatch
---
## Use the Digital Crown to control sprite movement

Welcome to my new WatchKit tutorial. Today I'll show that it is possible to use the Apple Watch as a gaming platform. First let's look back to the first WatchKit versions. They have been very limited in terms of available input controls. Using alternative hardware stuff like the Digital Crown was not supported. A typical game was usually built with a number of WkInterfaceButtons and looked like this:

[![15 Puzzle](/assets/wp-content/uploads/2016/04/Simulator-Screen-Shot-23-Apr-2016-09.40.13-1-240x300.jpg)](https://itunes.apple.com/app/15-puzzle-game-for-watch-phone/id997514879?l=en&mt=8)[![15 Puzzle](/assets/wp-content/uploads/2016/04/WatchGame2.png)](https://itunes.apple.com/app/15-puzzle-game-for-watch-phone/id997514879?l=en&mt=8)

Since WatchKit 2 it is possible to use the Digital Crown for custom apps. This provides way more possibilities for great games, like this [Watch Ping Pong](https://itunes.apple.com/app/watch-ping-pong/id1039082864?l=en&mt=8) version created by me. I'll publish the Source Code as OpenSource in my GitHub repository, once I have reached 1000 downloads. Currently only 980 to go ;-)

[![ Watch Ping Pong](/assets/wp-content/uploads/2016/04/WatchPingPongGif.gif)](https://itunes.apple.com/app/watch-ping-pong/id1039082864?l=en&mt=8)

I have a quick calculation for you, if you think 0.99$ is expensive: It took me around 30 hours to write the game. 20 downloads generate around 19,80$ earnings. Apple takes one third means 13,20$ remaining for me.  **= > Whoa! I've earned 0,44$ per hour ;-)** Don't get me wrong. I'm not expecting to get rich with my Apps. I'm writing this Blog and and my games only for fun.

### **But now, let's start with the tutorial:**

Goal is to create the racket at the left side and use the digital crown to move it up and down.

#### 1\. Open XCode and create a new WatchKit project:

[![WatchGame1](/assets/wp-content/uploads/2016/04/WatchGame1-300x211.png)](/assets/wp-content/uploads/2016/04/WatchGame1.png)

Disable the checkmark on 'Include Notification Scene':

[![WatchGameBlog2](/assets/wp-content/uploads/2016/04/WatchGameBlog2-300x212.png)](/assets/wp-content/uploads/2016/04/WatchGameBlog2.png)

#### 2\. Create the UserInterface:

Open the WatchKit Storyboard: [![WatchGameBlog3](/assets/wp-content/uploads/2016/04/WatchGameBlog3-1-300x135.jpg)](/assets/wp-content/uploads/2016/04/WatchGameBlog3-1.jpg)

Add a WKInterfaceGroup and below a WKInterfaceImage and a WKInterfacePicker to the InterfaceController:

[![WatchGameBlog4](/assets/wp-content/uploads/2016/04/WatchGameBlog4-1-300x140.jpg)](/assets/wp-content/uploads/2016/04/WatchGameBlog4-1.jpg)

Change the size of the group and the Image to fullscreen:

[![WatchGameBlog5](/assets/wp-content/uploads/2016/04/WatchGameBlog5-300x112.png)](/assets/wp-content/uploads/2016/04/WatchGameBlog5.png)

[![WatchGameBlog6](/assets/wp-content/uploads/2016/04/WatchGameBlog6-300x93.png)](/assets/wp-content/uploads/2016/04/WatchGameBlog6.png)

Change the radius of the group to 0:

[![WatchGameBlog7](/assets/wp-content/uploads/2016/04/WatchGameBlog7-300x92.png)](/assets/wp-content/uploads/2016/04/WatchGameBlog7.png)

The WKInterfacePicker will only be used to connect our interface with the digital crown. It is not necessary that it is visible on the screen.

### 3\. Connect the UI Classes with the InterfaceController:

Create an IBOutlet for 'Image' and 'Picker':

[![WatchGameBlog8](/assets/wp-content/uploads/2016/04/WatchGameBlog8-300x156.png)](/assets/wp-content/uploads/2016/04/WatchGameBlog8.png)

 

[![WatchGameBlog9](/assets/wp-content/uploads/2016/04/WatchGameBlog9-300x139.png)](/assets/wp-content/uploads/2016/04/WatchGameBlog9.png)

Create an IBAction for the 'Picker':

[![WatchGameBlog10](/assets/wp-content/uploads/2016/04/WatchGameBlog10-300x153.png)](/assets/wp-content/uploads/2016/04/WatchGameBlog10.png)

The result in your code should look like this:

@IBOutlet var picker: WKInterfacePicker!

@IBOutlet var image: WKInterfaceImage!

@IBAction func pick(value: Int) {}

### 4\. Implement the logic:

Now everything is setup and we can start implementing the logic. The picker outlet/action will provide the access to the digital crown. It must be initialized with some values first. Add this code snippet to the method willActivate():

 

override func willActivate() {

// This method is called when watch view controller is about to be visible to user

super.willActivate()

// Initialize picker with 10 items to detect state changes of the digital crown

var pickerItems: [WKPickerItem] = []

for _ in 0 ..< 10 {

let pickerItem = WKPickerItem()

pickerItem.title = ""

pickerItem.caption = ""

pickerItems.append(pickerItem)

}

picker.setItems(pickerItems)

picker.setSelectedItemIndex(4)

}

Move the racket overtime the picker changes:

@IBAction func pick(value: Int) {

// Create the graphics context

let size = CGSizeMake(100, 100)

UIGraphicsBeginImageContext(size)

let context = UIGraphicsGetCurrentContext()

// Setup for the path style

CGContextSetStrokeColorWithColor(context, UIColor.whiteColor().CGColor)

CGContextSetLineWidth(context, 2.0)

// Draw racket

CGContextBeginPath (context);

CGContextMoveToPoint(context, 80, CGFloat(value + 1) * 10);

CGContextAddLineToPoint(context, 80, CGFloat(value) * 10)

CGContextStrokePath(context);

// Convert to an UIImage

let cgimage = CGBitmapContextCreateImage(context);

let uiimage = UIImage(CGImage: cgimage!)

// End the graphics context

UIGraphicsEndImageContext()

// Assign on WKInterfaceImage

image.setImage(uiimage)

}

Now you can run the App and play with the crown and the racket. The result should look like this:

[![WatchGameDemoGif](/assets/wp-content/uploads/2016/04/WatchGameDemoGif.gif)](/assets/wp-content/uploads/2016/04/WatchGameDemoGif.gif)

That's all for today.

If you want to support me, please download my Apps from the Apple AppStore.

[![AppStore Stefan](/assets/wp-content/uploads/2015/11/AppStore1.png)](https://itunes.apple.com/developer/stefan-josten/id949662361)

Cheers,

Stefan

 

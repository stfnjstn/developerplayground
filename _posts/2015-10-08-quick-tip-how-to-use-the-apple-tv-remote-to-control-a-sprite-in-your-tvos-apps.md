---
layout: post
permalink: /quick-tip-how-to-use-the-apple-tv-remote-to-control-a-sprite-in-your-tvos-apps/
title: 'Quick Tip: How to use the Apple TV remote to control a sprite in your TVOS
  Apps'
seo_title: Use the Apple TV remote to control a sprite in your TVOS Apps
description: Use the Apple TV remote control to move a sprite in tvOS with SpriteKit
  and SWIFT
date: 2015-10-08 21:06:15 -0000
last_modified_at: 2020-05-27 16:40:56 -0000
publish: true
pin: false
image:
  path: /assets/wp-content/uploads/2015/10/IMG_2350.jpg
  alt: AppleTV Tutorial
categories:
- Apple TV
- SpriteKit
- SWIFT
- tvOS
tags:
- AppleTV
---
## How to use the Apple TV remote to control a sprite in your TVOS Apps

Since my Apple TV Developer kit arrived one week ago I had plenty of time to try certain things. I will blog about some of my prototypes in the next days.

[![Swift Tutorial Apple TV remote 1](/assets/wp-content/uploads/2015/10/Screen-Shot-2015-10-01-at-20.12.48-1.jpg)](/assets/wp-content/uploads/2015/10/Screen-Shot-2015-10-01-at-20.12.48-1.jpg)

Today I'll will focus again on the remote control. It provides, especially in combination with SpriteKit, a simple and very natural way to control a sprite on the screen. For a natural sprite movement the approach of my todays post is much better, the my [article about gesture recognition](/quick-tip-how-to-use-the-remote-control-in-your-tvos-apps-for-apple-tv-in-swift) on the AppleTV.

Let's start...

### 1\. Download the XCode 7.1 Beta from the [Apple Developer Portal](https://developer.apple.com/xcode/download/):

[![Swift Tutorial Apple TV remote 2](/assets/wp-content/uploads/2015/10/2-1.jpg)](/assets/wp-content/uploads/2015/10/2-1.jpg)

#### 2\. Create a new project:

[![Swift Tutorial Apple TV remote 3](/assets/wp-content/uploads/2015/10/3.png)](/assets/wp-content/uploads/2015/10/3.png)

[![Swift Tutorial Apple TV remote 4](/assets/wp-content/uploads/2015/10/4.png)](/assets/wp-content/uploads/2015/10/4.png)

#### 3\. Open GameViewController.swift

[![Swift Tutorial Apple TV remote 5](/assets/wp-content/uploads/2015/10/5-1.jpg)](/assets/wp-content/uploads/2015/10/5-1.jpg)

****

Change the scale mode from in viewDidLoad from

scene.scaleMode = .AspectFill

to

scene.scaleMode = .ResizeFill

#### 4\. Open GameScene.swift

Override the didMoveToView method with this snippet to create a sprite in the middle of the screen:

[![Swift Tutorial Apple TV remote 6](/assets/wp-content/uploads/2015/10/6-1.jpg)](/assets/wp-content/uploads/2015/10/6-1.jpg)

// Global property to store the sprite object

let sprite = SKSpriteNode(imageNamed:"Spaceship")

override func didMoveToView(view: SKView) {

sprite.yScale = 0.2

sprite.xScale = 0.2

sprite.position = CGPoint(x:CGRectGetMidX(self.frame), y:CGRectGetMidY(self.frame))

self.addChild(sprite)

}

#### 5\. Add the code to handle the sprite movement

Replace the touchesBegan method with this snippet to persist the initial touch position:

// Persist the initial touch position of the remote

var touchPositionX: CGFloat = 0.0

var touchPositionY: CGFloat = 0.0

override func touchesBegan(touches: Set<UITouch>, withEvent event: UIEvent?) {

for touch in touches {

touchPositionX = touch.locationInNode(self).x

touchPositionY = touch.locationInNode(self).y

}

}

The touchedMoved method implements the logic to move the sprite on the screen:

override func touchesMoved(touches: Set<UITouch>, withEvent event: UIEvent?) {

for touch in touches {

let location = touch.locationInNode(self)

if touchPositionX != 0.0 && touchPositionY != 0.0 {

// Calculate the movement on the remote

let deltaX = touchPositionX \- location.x

let deltaY = touchPositionY \- location.y

// Calculate the new Sprite position

var x = sprite.position.x \- deltaX

var y = sprite.position.y \- deltaY

// Check if the sprite will leave the screen

if x < 0 {

x = 0

} else if x > self.frame.width {

x = self.frame.width

}

if y < 0 {

y = 0

} else if y > self.frame.height {

y = self.frame.height

}

// Move the sprite

sprite.position = CGPoint(x: x, y: y)

}

// Persist latest touch position

touchPositionY = location.y

touchPositionX = location.x

}

}

#### 6\. Now let's move the sprite around and start the App

[![Swift Tutorial Apple TV remote 7](/assets/wp-content/uploads/2015/10/7-1.jpg)](/assets/wp-content/uploads/2015/10/7-1.jpg)

If you try this in the Simulator you have to press the option key (alt) on you Mac keyboard and move the mouse around on the touch area of the remote control window. No mouse clicks!!!

That's all for today.

Cheers,  
Stefan

[![AppStore Stefan](/assets/wp-content/uploads/2015/10/AppStore.png)](https://itunes.apple.com/developer/stefan-josten/id949662361)

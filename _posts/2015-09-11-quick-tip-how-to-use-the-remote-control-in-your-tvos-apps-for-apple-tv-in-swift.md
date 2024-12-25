---
layout: post
permalink: /quick-tip-how-to-use-the-remote-control-in-your-tvos-apps-for-apple-tv-in-swift/
title: 'Quick Tip: How to use the remote control in your TVOS Apps for Apple TV in
  SWIFT'
seo_title: Use the remote control in your TVOS Apps for Apple TV in SWIFT
description: 'SWIFT Tutorial: Use the Apple TV remote control as a game controller
  to move a sprite in tvOS using SpriteKit and SWIFT.'
date: 2015-09-11 21:13:00 -0000
last_modified_at: 2020-05-27 16:40:56 -0000
publish: true
pin: false
image:
  path: /assets/2015/10/Screen-Shot-2015-10-01-at-20.12.48-1.jpg
categories:
- SpriteKit
- SWIFT
- tvOS
tags:
- AppleTV
---
## How to use the remote control in your tvOS Apps for Apple TV in SWIFT

There are already dozens of 'Hello world' tutorials published for the new Apple tvOS, so let's do something different. I'll show how to use the remote control to move a sprite on Apple TV. It was surprisingly easy and took me only 10 minutes to implement:

### 1. Download the XCode 7.1 Beta from the [Apple Developer Portal](https://developer.apple.com/xcode/download/):

![Download XCode 7.1 Beta](/assets/2015/09/Screen-Shot-2015-09-11-at-00.01.17-1.jpg)

#### 2. Create a new project:

![tvOS Create new project](/assets/2015/09/Screen-Shot-2015-09-10-at-23.59.18.png) ![Create tvOS project](/assets/2015/09/Screen-Shot-2015-09-11-at-00.06.33.png)

#### 3. Open GameScene.swift:

![Create tvOS SpriteKit scene](/assets/2015/09/Screen-Shot-2015-09-11-at-00.03.18-1.jpg)

#### 4. Replace the complete code with this snippet:

```swift
import SpriteKit

class GameScene: SKScene {
  let sprite = SKSpriteNode(imageNamed:"Spaceship")

  override func didMoveToView(view: SKView) {
    /* Setup your scene here */
    // Add Sprite
    sprite.xScale = 0.5
    sprite.yScale = 0.5
    sprite.position = CGPoint(x:CGRectGetMidX(self.frame), y:CGRectGetMidY(self.frame))
    self.addChild(sprite)

    // Register Swipe Events
    let swipeRight:UISwipeGestureRecognizer = UISwipeGestureRecognizer(target: self, action: Selector("swipedRight:"))
    swipeRight.direction = .Right
    view.addGestureRecognizer(swipeRight)
    let swipeLeft:UISwipeGestureRecognizer = UISwipeGestureRecognizer(target: self, action: Selector("swipedLeft:"))
    swipeLeft.direction = .Left
    view.addGestureRecognizer(swipeLeft)
    let swipeUp:UISwipeGestureRecognizer = UISwipeGestureRecognizer(target: self, action: Selector("swipedUp:"))
    swipeUp.direction = .Up
    view.addGestureRecognizer(swipeUp)
    let swipeDown:UISwipeGestureRecognizer = UISwipeGestureRecognizer(target: self, action: Selector("swipedDown:"))
    swipeDown.direction = .Down
    view.addGestureRecognizer(swipeDown)
  }

  // Handle Swipe Events
  func swipedRight(sender:UISwipeGestureRecognizer){
    sprite.position = CGPoint(x: sprite.position.x \+ 10, y: sprite.position.y)
  }

  func swipedLeft(sender:UISwipeGestureRecognizer){
    sprite.position = CGPoint(x: sprite.position.x \- 10, y: sprite.position.y)
  }

  func swipedUp(sender:UISwipeGestureRecognizer){
    sprite.position = CGPoint(x: sprite.position.x, y: sprite.position.y+10)
  }

  func swipedDown(sender:UISwipeGestureRecognizer){
    sprite.position = CGPoint(x: sprite.position.x, y: sprite.position.y-10)
  }

  override func update(currentTime: CFTimeInterval) {
    /*Called before each frame is rendered*/
  }
}
```

#### 5. Start the Simulator:

![Start tvOS Simulator](/assets/2015/09/Screen-Shot-2015-09-11-at-00.06.44.png)

#### 6. Show the remote control:

![tvOS Simulator Remote Control](/assets/2015/09/Screen-Shot-2015-09-11-at-00.08.32-1.jpg)

#### 7. Move the sprite around:

This was the most confusing part and costs me some minutes. You have to press the option key (alt) on you Mac keyboard and move the mouse around on the touch area of the remote control window. No mouse clicks!!!

![tvOS Simulator and Remote Control](/assets/2015/09/Screen-Shot-2015-09-11-at-00.08.58-1.jpg)

That's all for today.

Cheers,  
Stefan

[![AppStore](/assets/2015/11/AppStore1.png)](https://itunes.apple.com/us/developer/stefan-josten/id949662361)

---
layout: post
permalink: /quick-tip-endless-scrolling-spritekit-swift-part-2-4/
title: 'Quick Tip: Endless scrolling tutorial with SpriteKit and SWIFT (Part 2 of
  2)'
description: 'Short scrolling tutorial: Implementing an endless background scrolling
  with SpriteKit and SWIFT including ease in/out animations.'
date: 2015-11-24 22:50:53 -0000
last_modified_at: 2020-05-27 16:40:56 -0000
publish: true
pin: false
image:
  path: /assets/2015/11/Scrolling.jpg
  alt: Scrolling tutorial
categories:
- Parallax Effect
- Scrolling
- SWIFT
tags:
- Scrolling
- SpriteKit
---
## Natural endless scrolling with easing

Welcome to my scrolling tutorial:

  * [Part 1](/quick-tip-endless-scrolling-with-spritekit-and-swift): Endless scrolling with background tiles
  * [Part 2](/quick-tip-endless-scrolling-spritekit-swift-part-2-4): Natural endless scrolling with easing

In [part one](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-4-collision-detection43) I showed how to implement endless scrolling. This is working fine, but there is still room for improvements. The scrolling starts immediately with full speed and also stops directly after the touch ends. A more natural movement would be to increase and decrease the speed slowly, till the target speed is reached or the movement is stopped. These is also known as [ease in or ease out](https://developers.google.com/web/fundamentals/design-and-ui/animations/the-basics-of-easing) animation. Thank you to hamobi who helped me with my [Stackoverflow question](http://stackoverflow.com/questions/33721183/ease-out-animation-for-skspritenode) for finding the right solution. To give you an impression compare the two videos: 

### Without Easing:
[![Video](/assets/Videos/uYVqG8Y8rLU.png)](https://youtu.be/uYVqG8Y8rLU)

### With Easing:
[![Video](/assets/Videos/k1m1JH7yYAw.png)](https://youtu.be/k1m1JH7yYAw)

### First repeat the steps from [Part 1 ](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-4-collision-detection43)

The main difference is the calculation of the speed which is done in the scroll function:

```swift
// Calculate the new speed with the easing function (New speed is influence by current speed)
let newSpeed = (currentSpeed \+ (speed - currentSpeed) * easeOutfactor)
```

### Open GameScene.swift:

[![SpriteKit scrolling tutorial](/assets/2015/11/Screen-Shot-2015-11-13-at-18.14.431-1.jpg)](/assets/2015/11/Screen-Shot-2015-11-13-at-18.14.431-1.jpg)

#### Replace the complete code with this snippet:

(For explanation check the comments inside the code snippet)

```swift
//
// GameScene.swift
// EndlessScrollingDemo
//
// Created by STEFAN JOSTEN on 13/11/15.
// Copyright (c) 2015 Stefan. All rights reserved.
//

import SpriteKit

class GameScene: SKScene {
  // Some global variables to preserve the state and store the touch positions
  var lastUpdateTime: CFTimeInterval?
  var currentSpeed: CGFloat = 0.0
  var nodeTileWidth: CGFloat = 0.0
  var xTouchCurrentPosition: CGFloat = 0.0
  var xTouchStartPosition: CGFloat = 0.0
  var xTouchDistance: CGFloat = 0.0

  // Some global constants to configure the speed
  let speedFactor:CGFloat = 5.0
  let easeOutfactor: CGFloat = 0.04

  // Declare the globaly needed sprite kit nodes
  var worldNode: SKSpriteNode?
  var spriteNode: SKSpriteNode?

  override func didMoveToView(view: SKView) {
    // Setup static background
    let backgroundNode = SKSpriteNode(imageNamed: "Background")
    backgroundNode.size = CGSize(width: self.frame.width, height: self.frame.height)
    backgroundNode.anchorPoint = CGPoint(x: 0, y: 0)
    backgroundNode.zPosition = -10
    self.addChild(backgroundNode)

    // Setup dynamic background tiles
    worldNode = SKSpriteNode()
    self.addChild(worldNode!)

    // Create the dynamic background tiles. Image of left and right node must be identical
    let leftNode = SKSpriteNode(imageNamed: "LeftTile")
    let middleNode = SKSpriteNode(imageNamed: "RightTile")
    let rightNode = SKSpriteNode(imageNamed: "LeftTile")

    // store this value globaly to avoid recalculations during each update call
    nodeTileWidth = leftNode.frame.size.width
    leftNode.anchorPoint = CGPoint(x: 0, y: 0)
    leftNode.position = CGPoint(x: 0, y: 0)
    middleNode.anchorPoint = CGPoint(x: 0, y: 0)
    middleNode.position = CGPoint(x: nodeTileWidth, y: 0)
    rightNode.anchorPoint = CGPoint(x: 0, y: 0)
    rightNode.position = CGPoint(x: nodeTileWidth * 2, y: 0)

    // Add the tiles to worldNode. worldNode is used to realize the scrolling
    worldNode!.addChild(leftNode)
    worldNode!.addChild(rightNode)
    worldNode!.addChild(middleNode)

    // Setup spaceship sprite
    spriteNode = SKSpriteNode(imageNamed: "Spaceship")
    spriteNode?.position = CGPoint(x:CGRectGetMidX(self.frame), y:CGRectGetMidY(self.frame))
    spriteNode?.xScale = 0.1
    spriteNode?.yScale = 0.1
    spriteNode?.zPosition = 10
    self.addChild(spriteNode!)
  }

  // Store the start touch position
  override func touchesBegan(touches: Set<UITouch>, withEvent event: UIEvent?) {
    for touch in touches {
      xTouchStartPosition = touch.locationInNode(self).x
    }
  }

  // Calculate the distance of the toch movement
  override func touchesMoved(touches: Set<UITouch>, withEvent event: UIEvent?) {
    for touch in touches {
      xTouchCurrentPosition = touch.locationInNode(self).x
      xTouchDistance = xTouchStartPosition \- xTouchCurrentPosition
    }
  }

  // Reset all movement states
  override func touchesEnded(touches: Set<UITouch>, withEvent event: UIEvent?) {
    xTouchCurrentPosition = 0.0
    xTouchDistance = 0.0
    xTouchStartPosition = 0.0
  }

  // SpriteKits gameloop function
  override func update(currentTime: CFTimeInterval) {
    // Scroll the background
    scroll(xTouchDistance, currentTime: currentTime)

    // Rotate sprite depending on direction
    if xTouchDistance > 0 {
      spriteNode?.zRotation = CGFloat(M_PI/2.0)
    } else if xTouchDistance < 0 {
      spriteNode?.zRotation = -CGFloat(M_PI/2.0)
    }
  }

  // Implement the scrolling
  func scroll(speed: CGFloat, currentTime: CFTimeInterval) {
    if lastUpdateTime != nil {

      // Calculate the new speed with the easing function (New speed is influence by current speed)
      let newSpeed = (currentSpeed \+ (speed - currentSpeed) * easeOutfactor)
      currentSpeed = newSpeed

      // Set the new x position depending on the timeframe since the last calls.
      // This is needed because spritekit cannot guarantee that the timeframe is allways the same

      worldNode!.position.x = worldNode!.position.x \+ newSpeed * CGFloat((currentTime - lastUpdateTime!)) * speedFactor

      // Check if right end is reached
      if worldNode!.position.x < -(2 * self.nodeTileWidth) {
        worldNode!.position.x = 0.0

      // Check if left end is reached
      } else if worldNode!.position.x > 0 {
        worldNode!.position.x = -(2 * self.nodeTileWidth)
      }
    }
    lastUpdateTime = currentTime
  }
}
```

You can download the complete sample from my [Github repository](https://github.com/stfnjstn/EndlessScrollingDemo/releases/tag/v0.2).

If you want to support me, please download my Apps from the Apple AppStore:

[![AppStore Stefan Josten](/assets/2015/11/AppStore1.png)](https://itunes.apple.com/developer/stefan-josten/id949662361)

 

That's all for today.

Cheers,   
Stefan

 

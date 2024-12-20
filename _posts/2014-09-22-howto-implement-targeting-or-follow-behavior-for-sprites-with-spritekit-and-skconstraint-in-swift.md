---
layout: post
permalink: /howto-implement-targeting-or-follow-behavior-for-sprites-with-spritekit-and-skconstraint-in-swift/
title: 'HowTo: Implement targeting or follow behaviour with SpriteKit and SKConstraint
  in SWIFT'
seo_title: 'HowTo: Implement targeting or follow behavior with SpriteKit and SKConstraint
  in SWIFT'
description: 'Tutorial about SpriteKit and SKConstraint: How to define orientation,
  distance and position constraints to implement a follow and targeting behavior.'
date: 2014-09-22 21:41:00 -0000
last_modified_at: 2020-05-27 16:40:55 -0000
publish: true
pin: false
categories:
- iOS
- SpriteKit
- SWIFT
tags: []
---
# **Welcome to Part 14 of my blog series about iOS game development: SpriteKit and SKConstraint**

At the developer conference WWDC, in June this year, Apple showed a new class in SpriteKit: SKConstraint. It can be used to define constraints for the orientation, the distance or the position of SpriteKit nodes. In my todays blog post I'll show how to use SKContraints to implement a follow and targeting behavior. I have updated this tutorial to XCode 6.3 and SWIFT 1.2!

[![](/assets/wp-content/uploads/2014/09/Foto-1.jpg)](/assets/wp-content/uploads/2014/09/Foto-1.jpg)

### 1. Create a new Project

[![follow1](/assets/wp-content/uploads/2014/09/follow1.png)](/assets/wp-content/uploads/2014/09/follow1.png)

[![follow2](/assets/wp-content/uploads/2014/09/follow2.png)](/assets/wp-content/uploads/2014/09/follow2.png)

[![follow3](/assets/wp-content/uploads/2014/09/follow3-1.jpg)](/assets/wp-content/uploads/2014/09/follow3-1.jpg)

### 2. Open the GameScene.swift file and remove the code for creating a label in didMoveToView:

```swift
override func didMoveToView(view: SKView) {
  /* Setup your scene here */
}
```

### 3. Create a global Sprite property:

```swift
var sprite = SKSpriteNode()
override func didMoveToView(view: SKView) {
  /*Setup your scene here*/
}
```

### 4. Create two sprites inside ``didMoveToView``:

```swift
self.backgroundColor = UIColor.blackColor()

// Create the followed sprite
sprite = SKSpriteNode(imageNamed:"Spaceship")
sprite.xScale = 0.15
sprite.yScale = 0.15
sprite.position = CGPointMake(100, 100)
self.addChild(sprite)

// Create the follower sprite
let followerSprite = SKSpriteNode(imageNamed:"Spaceship")
followerSprite.xScale = 0.15
followerSprite.yScale = 0.15
followerSprite.position = CGPointMake(150, 150)
followerSprite.color = UIColor.redColor()
followerSprite.colorBlendFactor=0.8
self.addChild(followerSprite)
```

### 5. Create two constraints inside didMoveToView:
One to specify the distance between the two Sprites to implement the follow behavior:

```swift
// Define Constraints for following behavior
let rangeToSprite = SKRange(lowerLimit: 100.0, upperLimit: 150.0)
let distanceConstraint = SKConstraint.distance(rangeToSprite, toNode: sprite)
```

One to specify the orientation of the follower Sprite to the followed Sprite:

```swift
// Define Constraints for orientation/targeting behavior
let rangeForOrientation = SKRange(lowerLimit: CGFloat(M_2_PI*7), upperLimit: CGFloat(M_2_PI*7))
let orientConstraint = SKConstraint.orientToNode(sprite, offset: rangeForOrientation)
````

Add the constraints to the follower Sprite:

```swift
// Add constraints
followerSprite.constraints = [orientConstraint, distanceConstraint]
````

### 6. Replace the code inside the touchesBegan method to implement the sprite movement:

```swift
override func touchesBegan(touches: Set<NSObject>, withEvent event: UIEvent) {
  /* Called when a touch begins */
  for touch in (touches as! Set<UITouch>) {
    let location = touch.locationInNode(self)
    let action = SKAction.moveTo(location, duration: 1)
    sprite.runAction(action)
  }
}

### 7. Start the project:

[![Video](/assets/wp-content/uploads/Videos/1A3TUvTiJfw.png)](https://youtu.be/1A3TUvTiJfw)

The source code can be found in my [GitHub repository](https://github.com/stfnjstn/SpriteKitConstraintDemo).

That's all for today.

Cheers,  
Stefan

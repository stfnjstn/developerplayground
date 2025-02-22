---
layout: post
permalink: /how-to-implement-a-space-shooter-with-spritekit-and-swift-part-3-create-a-hud/
title: Create a HUD
seo_title: 'Build a space shooter with SpriteKit and SWIFT: Create a HUD'
description: 'Part 3 of my tutorial series about implementing a simple space shooter
  game for iOS devices with SpriteKit in and SWIFT: Create a HUD'
date: 2014-11-19 20:52:00 -0000
last_modified_at: 2020-05-27 16:40:53 -0000
publish: true
pin: false
categories:
- HUD
- iOS
- SWIFT
tags: []
---
## How to implement a space shooter with SpriteKit and SWIFT - Part 3
### Adding a HUD with SpriteKit and SWIFT

[![Video](/assets/Videos/8d8MH_gXt84.png)](https://youtu.be/8d8MH_gXt84)

<div style="display: flex; justify-content: space-around; align-items: center;">
  <div style="text-align: center;">
    <a href="https://apps.apple.com/app/just-a-small-spaceshooter-lite/id949662362">
      <img src="/assets/Download.svg" alt="Download">
    </a>
    <p>Lite Version</p>
  </div>
  <div style="text-align: center;">
    <a href="https://apps.apple.com/app/just-a-small-spaceshooter/id1449062544">
      <img src="/assets/Download.svg" alt="Download" >
    </a>
    <p>Full Version</p>
  </div>
  <div></div>
</div>

#### Tutorial Overview: How to implement a space shooter with SpriteKit and SWIFT

* [Part 1](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-1): Initial project setup, sprite creation and movement using _SKAction_ and _SKConstraint_
* [Part 2](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-2): Adding enemies, bullets and shooting with _SKAction_ and _SKConstraint_
* [Part 3](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-3-create-a-hud): Adding a HUD with _SKLabelNode_ and _SKSpriteNode_
* [Part 4](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-4-collision-detection): Adding basic game logic and collision detection
* [Part 5](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-5-particles-and-sound): Adding particles and sound
* [Part 6](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-6-game-center-integration): _GameCenter_ integration
* [Part 7](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-7-iad-integration): _iAd_ integration
* [Part 8](/how-to-implement-in-app-purchase-for-your-ios-app-in-swift): In-App Purchases

### Add the HUD:

I'll add a simple HUD which shows the score, the remaining lifes and a pause button. As a starting point you can download the code from tutorial part 2 [here](https://github.com/stfnjstn/MySecondGame/releases/tag/v0.2). 

First of all let's fix a bug in the sample code of my last post. Open GameViewController.swift and move the code from viewDidLoad to viewDidAppear. This is necessary because the orientation change to landscape might not be completed. In this case width and height are inverted, if we determine them in viewDidLoad:

```swift
override func viewDidLoad() {
  super.viewDidLoad()
}

override func viewDidAppear(animated: Bool) {
  super.viewDidAppear(animated)

  // Detect the screensize
  var sizeRect = UIScreen.mainScreen().applicationFrame
  var width = sizeRect.size.width * UIScreen.mainScreen().scale
  var height = sizeRect.size.height * UIScreen.mainScreen().scale

  // Scene should be shown in fullscreen mode
  let scene = GameScene(size: CGSizeMake(width, height))

  // Configure the view.
  let skView = self.view as SKView
  skView.showsFPS = true
  skView.showsNodeCount = true

  /* Sprite Kit applies additional optimizations to improve rendering performance */
  skView.ignoresSiblingOrder = true
  
  /* Set the scale mode to scale to fit the window */
  scene.scaleMode = .AspectFill
  skView.presentScene(scene)
}
```

Now let's create the HUD: 

![Part 1](/assets/2014/11/3-1.png)

It contains 3 different elements :

  * Remaining lifes: Must be accessible outside of the createHUD method to enable extra life or life lost events. Stored in a global array of SKSpriteNodes. 


![Part 2](/assets/2014/11/3-2-1.jpg)

  * Pause button: A SKLabelNode which is placed in a transparent SKSpriteNode to increase the touchable area.


![Part 3](/assets/2014/11/3-3.png)

  * Score: Must be accessible outside of the createHUD method. Stored in a global SKLabelNode property.


![Part 4](/assets/2014/11/3-4.png)

To access the HUD elements add these global properties to GameScene.swift:

```swift
  /// HUD Global properties
  var lifeNodes : [SKSpriteNode] = []
  var remainingLifes = 3
  var scoreNode = SKLabelNode()
  var score = 0
```

To create a HUD add this method to GameScene.swift:

```swift
func createHUD() {
  // Create a root node with black background to position and group the HUD elemets
  // HUD size is relative to the screen resolution to handle iPad and iPhone screens
  var hud = SKSpriteNode(color: UIColor.blackColor(), size: CGSizeMake(self.size.width, self.size.height*0.05))
  hud.anchorPoint=CGPointMake(0, 0)
  hud.position = CGPointMake(0, self.size.height-hud.size.height)
  self.addChild(hud)

  // Display the remaining lifes
  // Add icons to display the remaining lifes
  // Reuse the Spaceship image: Scale and position releative to the HUD size
  let lifeSize = CGSizeMake(hud.size.height-10, hud.size.height-10)
  for(var i = 0; i<self.remainingLifes; i++) {
    var tmpNode = SKSpriteNode(imageNamed: "Spaceship")
    lifeNodes.append(tmpNode)
    tmpNode.size = lifeSize
    tmpNode.position=CGPointMake(tmpNode.size.width * 1.3 * (1.0 + CGFloat(i)), (hud.size.height-5)/2)
    hud.addChild(tmpNode)
  }

  // Pause button container and label
  // Needed to increase the touchable area
  // Names will be used to identify these elements in the touch handler
  var pauseContainer = SKSpriteNode()
  pauseContainer.position = CGPointMake(hud.size.width/1.5, 1)
  pauseContainer.size = CGSizeMake(hud.size.height*3, hud.size.height*2)
  pauseContainer.name = "PauseButtonContainer"
  hud.addChild(pauseContainer)

  var pauseButton = SKLabelNode()
  pauseButton.position = CGPointMake(hud.size.width/1.5, 1)
  pauseButton.text="I I"
  pauseButton.fontSize=hud.size.height
  pauseButton.horizontalAlignmentMode = SKLabelHorizontalAlignmentMode.Center
  pauseButton.name="PauseButton"
  hud.addChild(pauseButton)

  // Display the current score
  self.score = 0
  self.scoreNode.position = CGPointMake(hud.size.width-hud.size.width * 0.1, 1)
  self.scoreNode.text = "0"
  self.scoreNode.fontSize = hud.size.height
  hud.addChild(self.scoreNode)
}
```

To add the HUD to the screen add this line at the end of the didMoveToView method of GameScene.swift: 

```swift
// Add HUD
createHUD()
```

That's all for today. In my next part I'll add collision detection and a basic game logic for life lost, game over, pause, score behavior.
You can download the code from GitHub: [Part 3](https://github.com/stfnjstn/MySecondGame/releases/tag/v0.3) or the latest version [here](https://github.com/stfnjstn/MySecondGame/tree/master).
You can also download my prototyping App for this tutorial series:

<div style="display: flex; justify-content: space-around; align-items: center;">
  <div style="text-align: center;">
    <a href="https://apps.apple.com/app/just-a-small-spaceshooter-lite/id949662362">
      <img src="/assets/Download.svg" alt="Download">
    </a>
    <p>Lite Version</p>
  </div>
  <div style="text-align: center;">
    <a href="https://apps.apple.com/app/just-a-small-spaceshooter/id1449062544">
      <img src="/assets/Download.svg" alt="Download" >
    </a>
    <p>Full Version</p>
  </div>
  <div></div>
</div>

Cheers,   
Stefan

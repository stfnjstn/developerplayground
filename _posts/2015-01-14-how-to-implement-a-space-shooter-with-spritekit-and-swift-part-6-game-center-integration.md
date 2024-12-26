---
layout: post
permalink: /how-to-implement-a-space-shooter-with-spritekit-and-swift-part-6-game-center-integration/
title: Game Center Integration
seo_title: 'Build a space shooter with SpriteKit & SWIFT: Game Center'
description: 'Part 6 of my tutorial series about implementing a simple space shooter
  game for iOS devices with SpriteKit in and SWIFT: Game Center integration'
date: 2015-01-14 23:01:00 -0000
last_modified_at: 2020-05-27 16:40:54 -0000
publish: true
pin: false
image:
  path: /assets/2015/04/AppStore.png
categories:
- Game Development
- GameCenter
- iOS
- SWIFT
tags: []
---
## How to implement a space shooter with SpriteKit and SWIFT - Part 6
### Adding Game Center Integration:

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

### Overview: How to implement a space shooter with SpriteKit and SWIFT

* [Part 1](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-1): Initial project setup, sprite creation and movement using _SKAction_ and _SKConstraint_
* [Part 2](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-2): Adding enemies, bullets and shooting with _SKAction_ and _SKConstraint_
* [Part 3](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-3-create-a-hud): Adding a HUD with _SKLabelNode_ and _SKSpriteNode_
* [Part 4](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-4-collision-detection): Adding basic game logic and collision detection
* [Part 5](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-5-particles-and-sound): Adding particles and sound
* [Part 6](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-6-game-center-integration): _GameCenter_ integration
* [Part 7](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-7-iad-integration): _iAd_ integration
* [Part 8](/how-to-implement-in-app-purchase-for-your-ios-app-in-swift): In-App Purchases

Welcome to part 6 of my swift programming tutorial. In the previous parts we've created sprites, added movement, created enemies which follow our sprite, added bullets, a HUD, collision detection, sound and particle effects. Today I'll show how to integrate Game Center to add a global leaderboard.

The most complex part is doing configuration stuff in [iTunes Connect](https://itunesconnect.apple.com/). 3 from 4 steps of this tutorial are related to that. You need a paid Apple Developer Account to execute the next steps:

  * Upload our App to iTunes Connect 
  * Create a Leaderboard in iTunes Connect 
  * Create a Sandbox Test User in iTunes Connect
  * Coding 

**Let's start:**

###  1. Upload App to iTunes Connect 

Check, if XCode is set up properly with your Apple account data:

![GC1](/assets/2015/01/GC1-1.jpg)

Before submitting your app add appropriate app icons to your project. Otherwise iTunes Connect will reject your upload: 

![gc2](/assets/2015/01/gc2-1.jpg)

Enable Game Center in the Capabilities Tab of your project. Select your team profile and wait a few seconds till XCode has updated the project settings. 

![gc3](/assets/2015/01/gc3-1.jpg)

Create an Archive of your app: 

![gc4](/assets/2015/01/gc4-1.jpg)

Open the Organizer window: 

![gc5](/assets/2015/01/gc5-1.jpg)

![gc6](/assets/2015/01/gc6-1.jpg)

Click Submit choose your profile and submit your application to iTunesConnect

![gc7](/assets/2015/01/gc7.png)

If you see this error message you haven't created an AppId for your app in iTunesConnect: 

![gc8](/assets/2015/01/gc8.png)

Open [iTunesConnect](https://itunesconnect.apple.com/) in your browser, select MyApps, add a new app and fill out the required fields: 

![gc9](/assets/2015/01/gc9-1.jpg)
![gc10](/assets/2015/01/gc10.png)
![gc11](/assets/2015/01/gc11.png)
![gc12](/assets/2015/01/gc12.png)

Go back to XCode, open the Organizer window and submit your app again:

![gc13](/assets/2015/01/gc13.png)

![gc14](/assets/2015/01/gc14.png)

### 2. Create a Leaderboard in iTunesConnect 

Open [iTunesConnect](https://itunesconnect.apple.com/) and select your app: 

![gc15](/assets/2015/01/gc15.png)

Click on Game Center: 

![gc16](/assets/2015/01/gc16-1.jpg)

Select Single Game: 

![gc17](/assets/2015/01/gc17.png)

Select Add Leaderboard: 

![gc18](/assets/2015/01/gc18.png)

Choose Single Leaderboard: 

![gc19](/assets/2015/01/gc19.png)

Configure your Leaderboard: 

![gc20](/assets/2015/01/gc20.png)

Add at least one language: 

![gc21](/assets/2015/01/gc21.png)

![gc22](/assets/2015/01/gc22.png)

![gc23](/assets/2015/01/gc23.png)

Confirm your changes by selecting Done. Now back to XCode. 

### 3. Create a Sandbox Test User in iTunes Connect 

To test the Game Center integration inside your App you need to create one or more Sandbox Testers in iTunes Connect. More details about creating them can be found in the [Apple Documentation](https://developer.apple.com/library/ios/documentation/LanguagesUtilities/Conceptual/iTunesConnect_Guide/Chapters/SettingUpUserAccounts.html).  Open the Users and Roles section in iTunes Connect: 

![gc24](/assets/2015/01/gc24-1.jpg)

Choose the Sandbox Testers tab at the right and create at least one: 

![gc25](/assets/2015/01/gc25.png)

Fill out the required fields. You need a valid email account for this: 

![gc26](/assets/2015/01/gc26.png)

![gc27](/assets/2015/01/gc27.png)

### 4. Coding 

Comparing to the iTunes Connect stuff the code changes are simple. I'll implement it in GameViewController.swift and GameScene.swift. As the first code change import the GameKit Framework in both files: 

import GameKit

The next image shows the control flow of my game center integration: 

![gc28](/assets/2015/01/gc28-1.jpg)

#### Game Center initialization: 

Check if Game Center is available. Otherwise present the Login Screen:

![](/assets/2015/01/IMG_87151-1.jpg)

![](/assets/2015/01/IMG_87141-1.jpg)

Move the Scene declaration outside the viewDidAppear method to make it a global property. This is necessary because you need to access the scene outside of viewDidAppear:

```swift
class GameViewController: UIViewController, GKGameCenterControllerDelegate, GameSceneProtocol {
  var scene : GameScene?
  override func viewDidAppear(animated: Bool) {
  super.viewDidAppear(animated)
  ...

  // Create a fullscreen Scene object
  scene = GameScene(size: CGSizeMake(width, height))
  scene!.scaleMode = .AspectFill
  ...
```

To implement this behavior open GameViewController.swift and add a new method initGameCenter: 

```swift
// Initialize Game Center
func initGameCenter() {

  // Check if user is already authenticated in game center
  if GKLocalPlayer.localPlayer().authenticated == false {
    // Show the Login Prompt for Game Center
    GKLocalPlayer.localPlayer().authenticateHandler = {(viewController, error) -> Void in
      if viewController != nil {
        self.scene!.gamePaused = true
        self.presentViewController(viewController, animated: true, completion: nil)

        // Add an observer which calls 'gameCenterStateChanged' to handle a changed game center state
        let notificationCenter = NSNotificationCenter.defaultCenter()
        notificationCenter.addObserver(self, selector:"gameCenterStateChanged", name: "GKPlayerAuthenticationDidChangeNotificationName", object: nil)
      }
    }
  }
}
```

Add another method to GameViewController.swift which will be called by the observer created before in case of a changed game center change:

```swift
// Continue the Game, if GameCenter Authentication state
// has been changed (login dialog is closed)
func gameCenterStateChanged() {
  self.scene!.gamePaused = false
}
```

Finally call initGameCenter in the viewDidLoad method:

```swift
override func viewDidLoad() {
  super.viewDidLoad()

  // Initialize game center
  self.initGameCenter()
}
```

You can use your sandbox test user to test this on a device. Go to the Settings Dialog, open Game Center and click on Apple-ID. The current user must logout. Scroll down to the developer section and activate the Sandbox switch. Now start the game and login with your test user.

#### Submit a new leaderboard score:

Open GameScene.swift and change the type of the global score property from Integer:

```swift
var score = 0
```

to Int64, the type chosen for the leaderboard

```swift
var score : Int64 = 0
```

Add another global property to store a game over state:

```swift
var gameOver = false
```

Modify the update method to handle the new gameOver property:

```swift
override func update(currentTime: CFTimeInterval) {
  if !self.gamePaused && !self.gameOver {
    ...
  }
}
```

Add/Remove the red marked lines in the showGameOverAlert method of 

```swift
func showGameOverAlert() {
  self.gamePaused = true
  self.gameOver = true
  var alert = UIAlertController(title: "Game Over", message: "", preferredStyle: UIAlertControllerStyle.Alert)
  alert.addAction(UIAlertAction(title: "OK", style: UIAlertActionStyle.Default) { _ in
    // restore lifes in HUD
    self.remainingLifes=3
    for(var i = 0; i<3; i++) {
      self.lifeNodes[i].alpha=1.0
    }

    // reset score
    self.addLeaderboardScore(self.score)
    self.score=0
    self.scoreNode.text = String(0)
    self.gamePaused = true
  })
}
```

Add a new method addLeaderboardScore to submit a new score: 

```swift
func addLeaderboardScore(score: Int64) {
  var newGCScore = GKScore(leaderboardIdentifier: "MySecondGameLeaderboard")
  newGCScore.value = score
  GKScore.reportScores([newGCScore], withCompletionHandler: {(error) -> Void in
    if error != nil {
      println("Score not submitted")
      // Continue
      self.gameOver = false
    } else {
      // Notify the delegate to show the game center leaderboard:
      // Not implemented yet
    }
  })
}
```

#### Show the Game Center leaderboard after game over:

![GameOver](/assets/2015/01/IMG_87121-1.jpg)

The game center leaderboard can only be called/shown from a ViewController, not inside a SpriteKit Scene. To notify the container ViewController of our scene add a protocol to GameScene.swift:

```swift
// protocol to inform the delegate (GameViewController) about a game over situation
protocol GameSceneDelegate {
  func gameOver()

  }
```

Don't forget to create a global Delegate Property:

```swift
var gameCenterDelegate : GameSceneDelegate?
```

Modify addLeaderboardScore to notify the delegate:
```swift
func addLeaderboardScore(score: Int64) {
  var newGCScore = GKScore(leaderboardIdentifier: "MySecondGameLeaderboard")
  newGCScore.value = score
  GKScore.reportScores([newGCScore], withCompletionHandler: {(error) -> Void in
    if error != nil {
      println("Score not submitted")
      // Continue
      self.gameOver = false
    } else {
      // Notify the delegate to show the game center leaderboard
      self.gameCenterDelegate!.gameOver()
    }
  })
}
```

Open GameViewController.swift and add these protocols to the declaration of GameViewController:

```swift
class GameViewController: UIViewController, GameSceneDelegate, GKGameCenterControllerDelegate{
```

The first one is used by our game scene class to notify about a game over event. The second one is provided by GameKit to notify when the leaderboard has been closed.

Now set the Delegate property for the scene class:

```swift
override func viewDidAppear(animated: Bool) {
  ...

  // Create a fullscreen Scene object
  scene = GameScene(size: CGSizeMake(width, height))
  scene!.scaleMode = .AspectFill
  scene!.gameCenterDelegate = self
```

To show the leaderboard implement the gameOver protocol method:

```swift
// Show game center leaderboard
func gameOver() {
  var gcViewController = GKGameCenterViewController()
  gcViewController.gameCenterDelegate = self
  gcViewController.viewState = GKGameCenterViewControllerState.Leaderboards
  gcViewController.leaderboardIdentifier = "MySecondGameLeaderboard"

  // Show leaderboard
  self.presentViewController(gcViewController, animated: true, completion: nil)
}
```

To continue the game implement this protocol method:

```swift
// Continue the game after GameCenter is closed
func gameCenterViewControllerDidFinish(gameCenterViewController: GKGameCenterViewController!) {
  gameCenterViewController.dismissViewControllerAnimated(true, completion: nil)
  scene!.gameOver = false
}
```

That's all for today. You can download the code from GitHub: [Part 6](https://github.com/stfnjstn/MySecondGame/releases/tag/v0.6) or the [latest version](https://github.com/stfnjstn/MySecondGame/tree/master). In my next tutorial I'll show how to integrate Apples advertising framework iAD.  You can also download my prototyping App for this tutorial series: 

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

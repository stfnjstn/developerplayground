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
  path: /assets/wp-content/uploads/2015/04/AppStore.png
categories:
- Game Development
- GameCenter
- iOS
- SWIFT
tags: []
---
Adding Game Center Integration: How to implement a space shooter with SpriteKit and SWIFT - Part 6

[![](/assets/wp-content/uploads/2015/01/AppStore.png)](https://itunes.apple.com/us/app/yet-another-spaceshooter/id949662362?mt=8)

### Overview: How to implement a space shooter with SpriteKit and SWIFT

  * [Part 1](https://developerplayground.net/?p=14): Initial project setup, sprite creation and movement using SKAction and SKConstraint
  * [Part 2](https://developerplayground.net/?p=13): Adding enemies, bullets and shooting with SKAction and SKConstraint
  * [Part 3](https://developerplayground.net/?p=12): Adding a HUD with SKLabelNode and SKSpriteNode
  * [Part 4](https://developerplayground.net/?p=11): Adding basic game logic and collision detection
  * [Part 5](https://developerplayground.net/?p=10): Adding particles and sound 
  * [Part 6](https://developerplayground.net/?p=9): GameCenter integration
  * [Part 7](https://developerplayground.net/?p=8): iAd integration
  * [Part 8](https://developerplayground.net/?p=5): In-App Purchases



Welcome to part 6 of my swift programming tutorial. In the previous parts we've created sprites, added movement, created enemies which follow our sprite, added bullets, a HUD, collision detection, sound and particle effects. Today I'll show how to integrate Game Center to add a global leaderboard.

The most complex part is doing configuration stuff in [iTunes Connect](https://itunesconnect.apple.com/). 3 from 4 steps of this tutorial are related to that. You need a paid Apple Developer Account to execute the next steps:

  * Upload our App to iTunes Connect 
  * Create a Leaderboard in iTunes Connect 
  * Create a Sandbox Test User in iTunes Connect
  * Coding 

**Let's start:**

###  1\. Upload App to iTunes Connect 

Check, if XCode is set up properly with your Apple account data:

[![GC1](/assets/wp-content/uploads/2015/01/GC1-1-300x107.jpg)](/assets/wp-content/uploads/2015/01/GC1-1.jpg)

Before submitting your app add appropriate app icons to your project. Otherwise iTunes Connect will reject your upload: 

[![gc2](/assets/wp-content/uploads/2015/01/gc2-1-300x102.jpg)](/assets/wp-content/uploads/2015/01/gc2-1.jpg)

Enable Game Center in the Capabilities Tab of your project. Select your team profile and wait a few seconds till XCode has updated the project settings. 

[![gc3](/assets/wp-content/uploads/2015/01/gc3-1-300x62.jpg)](/assets/wp-content/uploads/2015/01/gc3-1.jpg)

Create an Archive of your app: 

[![gc4](/assets/wp-content/uploads/2015/01/gc4-1-195x300.jpg)](/assets/wp-content/uploads/2015/01/gc4-1.jpg)

Open the Organizer window: 

[![gc5](/assets/wp-content/uploads/2015/01/gc5-1-300x197.jpg)](/assets/wp-content/uploads/2015/01/gc5-1.jpg)

[![gc6](/assets/wp-content/uploads/2015/01/gc6-1-300x171.jpg)](/assets/wp-content/uploads/2015/01/gc6-1.jpg)

Click Submit choose your profile and submit your application to iTunesConnect

[![gc7](/assets/wp-content/uploads/2015/01/gc7-300x186.png)](/assets/wp-content/uploads/2015/01/gc7.png)

If you see this error message you haven't created an AppId for your app in iTunesConnect: 

[![gc8](/assets/wp-content/uploads/2015/01/gc8-300x181.png)](/assets/wp-content/uploads/2015/01/gc8.png)

Open [iTunesConnect](https://itunesconnect.apple.com/) in your browser, select MyApps, add a new app and fill out the required fields: 

[![gc9](/assets/wp-content/uploads/2015/01/gc9-1.jpg)](/assets/wp-content/uploads/2015/01/gc9-1.jpg) [![gc10](/assets/wp-content/uploads/2015/01/gc10.png)](/assets/wp-content/uploads/2015/01/gc10.png) [![gc11](/assets/wp-content/uploads/2015/01/gc11-300x145.png)](/assets/wp-content/uploads/2015/01/gc11.png) [![gc12](/assets/wp-content/uploads/2015/01/gc12-300x95.png)](/assets/wp-content/uploads/2015/01/gc12.png)

Go back to XCode, open the Organizer window and submit your app again:

[![gc13](/assets/wp-content/uploads/2015/01/gc13-300x180.png)](/assets/wp-content/uploads/2015/01/gc13.png)

[![gc14](/assets/wp-content/uploads/2015/01/gc14-300x184.png)](/assets/wp-content/uploads/2015/01/gc14.png)

### 2\. Create a Leaderboard in iTunesConnect 

Open [iTunesConnect](https://itunesconnect.apple.com/) and select your app: 

[![gc15](/assets/wp-content/uploads/2015/01/gc15-210x300.png)](/assets/wp-content/uploads/2015/01/gc15.png)

Click on Game Center: 

[![gc16](/assets/wp-content/uploads/2015/01/gc16-1-300x94.jpg)](/assets/wp-content/uploads/2015/01/gc16-1.jpg)

Select Single Game: 

[![gc17](/assets/wp-content/uploads/2015/01/gc17-300x118.png)](/assets/wp-content/uploads/2015/01/gc17.png)

Select Add Leaderboard: 

[![gc18](/assets/wp-content/uploads/2015/01/gc18-300x172.png)](/assets/wp-content/uploads/2015/01/gc18.png)

Choose Single Leaderboard: 

[![gc19](/assets/wp-content/uploads/2015/01/gc19-300x96.png)](/assets/wp-content/uploads/2015/01/gc19.png)

Configure your Leaderboard: 

[![gc20](/assets/wp-content/uploads/2015/01/gc20-300x122.png)](/assets/wp-content/uploads/2015/01/gc20.png)

Add at least one language: 

[![gc21](/assets/wp-content/uploads/2015/01/gc21-300x140.png)](/assets/wp-content/uploads/2015/01/gc21.png)

[![gc22](/assets/wp-content/uploads/2015/01/gc22-300x90.png)](/assets/wp-content/uploads/2015/01/gc22.png)

[![gc23](/assets/wp-content/uploads/2015/01/gc23-300x103.png)](/assets/wp-content/uploads/2015/01/gc23.png)

Confirm your changes by selecting Done. Now back to XCode. 

### 3\. Create a Sandbox Test User in iTunes Connect 

To test the Game Center integration inside your App you need to create one or more Sandbox Testers in iTunes Connect. More details about creating them can be found in the [Apple Documentation](https://developer.apple.com/library/ios/documentation/LanguagesUtilities/Conceptual/iTunesConnect_Guide/Chapters/SettingUpUserAccounts.html).  Open the Users and Roles section in iTunes Connect: 

[![gc24](/assets/wp-content/uploads/2015/01/gc24-1.jpg)](/assets/wp-content/uploads/2015/01/gc24-1.jpg)

Choose the Sandbox Testers tab at the right and create at least one: 

[![gc25](/assets/wp-content/uploads/2015/01/gc25-300x55.png)](/assets/wp-content/uploads/2015/01/gc25.png)

Fill out the required fields. You need a valid email account for this: 

[![gc26](/assets/wp-content/uploads/2015/01/gc26-300x178.png)](/assets/wp-content/uploads/2015/01/gc26.png)

[![gc27](/assets/wp-content/uploads/2015/01/gc27-300x76.png)](/assets/wp-content/uploads/2015/01/gc27.png)

### 4\. Coding 

Comparing to the iTunes Connect stuff the code changes are simple. I'll implement it in GameViewController.swift and GameScene.swift. As the first code change import the GameKit Framework in both files: 

import GameKit

The next image shows the control flow of my game center integration: 

[![gc28](/assets/wp-content/uploads/2015/01/gc28-1-195x300.jpg)](/assets/wp-content/uploads/2015/01/gc28-1.jpg)

#### Game Center initialization: 

Check if Game Center is available. Otherwise present the Login Screen:

[![](/assets/wp-content/uploads/2015/01/IMG_87151-1.jpg)](/assets/wp-content/uploads/2015/01/IMG_87151-1.jpg)

[![](/assets/wp-content/uploads/2015/01/IMG_87141-1.jpg)](/assets/wp-content/uploads/2015/01/IMG_87141-1.jpg)

Move the Scene declaration outside the viewDidAppear method to make it a global property. This is necessary because you need to access the scene outside of viewDidAppear:

class GameViewController: UIViewController, GKGameCenterControllerDelegate, GameSceneProtocol {

var scene : GameScene?

override func viewDidAppear(animated: Bool) {

super.viewDidAppear(animated)

...

// Create a fullscreen Scene object

scene = GameScene(size: CGSizeMake(width, height))

scene!.scaleMode = .AspectFill

...

To implement this behavior open GameViewController.swift and add a new method initGameCenter: 

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

Add another method to GameViewController.swift which will be called by the observer created before in case of a changed game center change:

// Continue the Game, if GameCenter Authentication state

// has been changed (login dialog is closed)

func gameCenterStateChanged() {

self.scene!.gamePaused = false

}

Finally call initGameCenter in the viewDidLoad method:

override func viewDidLoad() {

super.viewDidLoad()

// Initialize game center

self.initGameCenter()

}

You can use your sandbox test user to test this on a device. Go to the Settings Dialog, open Game Center and click on Apple-ID. The current user must logout. Scroll down to the developer section and activate the Sandbox switch. Now start the game and login with your test user.

#### Submit a new leaderboard score:

Open GameScene.swift and change the type of the global score property from Integer:

var score = 0

to Int64, the type chosen for the leaderboard

var score : Int64 = 0

Add another global property to store a game over state:

var gameOver = false

Modify the update method to handle the new gameOver property:

override func update(currentTime: CFTimeInterval) {

if !self.gamePaused && !self.gameOver {

...

}

}

Add/Remove the red marked lines in the showGameOverAlert method of 

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

Add a new method addLeaderboardScore to submit a new score: 

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

#### Show the Game Center leaderboard after game over:

[![](/assets/wp-content/uploads/2015/01/IMG_87121-1.jpg)](/assets/wp-content/uploads/2015/01/IMG_87121-1.jpg)

The game center leaderboard can only be called/shown from a ViewController, not inside a SpriteKit Scene. To notify the container ViewController of our scene add a protocol to GameScene.swift:

// protocol to inform the delegate (GameViewController) about a game over situation

protocol GameSceneDelegate {

func gameOver()

}

Don't forget to create a global Delegate Property:

var gameCenterDelegate : GameSceneDelegate?

Modify addLeaderboardScore to notify the delegate:

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

Open GameViewController.swift and add these protocols to the declaration of GameViewController:

class GameViewController: UIViewController, GameSceneDelegate, GKGameCenterControllerDelegate{

The first one is used by our game scene class to notify about a game over event. The second one is provided by GameKit to notify when the leaderboard has been closed.

Now set the Delegate property for the scene class:

override func viewDidAppear(animated: Bool) {

...

// Create a fullscreen Scene object

scene = GameScene(size: CGSizeMake(width, height))

scene!.scaleMode = .AspectFill

scene!.gameCenterDelegate = self

To show the leaderboard implement the gameOver protocol method:

// Show game center leaderboard

func gameOver() {

var gcViewController = GKGameCenterViewController()

gcViewController.gameCenterDelegate = self

gcViewController.viewState = GKGameCenterViewControllerState.Leaderboards

gcViewController.leaderboardIdentifier = "MySecondGameLeaderboard"

// Show leaderboard

self.presentViewController(gcViewController, animated: true, completion: nil)

}

To continue the game implement this protocol method:

// Continue the game after GameCenter is closed

func gameCenterViewControllerDidFinish(gameCenterViewController: GKGameCenterViewController!) {

gameCenterViewController.dismissViewControllerAnimated(true, completion: nil)

scene!.gameOver = false

}

That's all for today. You can download the code from GitHub: [Part 6](https://github.com/stfnjstn/MySecondGame/releases/tag/v0.6) or the [latest version](https://github.com/stfnjstn/MySecondGame/tree/master). In my next tutorial I'll show how to integrate Apples advertising framework iAD.  You can also download my prototyping App for this tutorial series: 

[![](/assets/wp-content/uploads/2015/01/AppStore.png)](https://itunes.apple.com/us/app/yet-another-spaceshooter/id949662362?mt=8)

Cheers,    
Stefan 
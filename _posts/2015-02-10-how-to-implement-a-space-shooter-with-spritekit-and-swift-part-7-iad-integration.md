---
layout: post
permalink: /how-to-implement-a-space-shooter-with-spritekit-and-swift-part-7-iad-integration/
title: iAd Integration
seo_title: 'Build a space shooter in SpriteKit & SWIFT: iAd integration'
description: 'Part 7 of my tutorial series about implementing a simple space shooter
  game for iOS devices with SpriteKit in and SWIFT: Earn money with iAd integration'
date: 2015-02-10 06:33:00 -0000
last_modified_at: 2020-05-27 16:40:55 -0000
publish: true
pin: false
image:
  path: /assets/wp-content/uploads/2015/04/AppStore.png
categories:
- AdSense and Admob
- iOS
- SWIFT
tags:
- iAD
---
## How to implement a space shooter with SpriteKit and SWIFT - Part 7
### Adding iAd Integration:

TODO Video https://youtu.be/8d8MH_gXt84

[![](/assets/wp-content/uploads/2015/04/AppStore.png)](https://itunes.apple.com/us/app/yet-another-spaceshooter/id949662362?mt=8)

#### Tutorial Overview: How to implement a space shooter with SpriteKit and SWIFT

* [Part 1](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-1): Initial project setup, sprite creation and movement using _SKAction_ and _SKConstraint_
* [Part 2](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-2): Adding enemies, bullets and shooting with _SKAction_ and _SKConstraint_
* [Part 3](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-3-create-a-hud): Adding a HUD with _SKLabelNode_ and _SKSpriteNode_
* [Part 4](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-4-collision-detection): Adding basic game logic and collision detection
* [Part 5](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-5-particles-and-sound): Adding particles and sound
* [Part 6](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-6-game-center-integration): _GameCenter_ integration
* [Part 7](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-7-iad-integration): _iAd_ integration
* [Part 8](/how-to-implement-in-app-purchase-for-your-ios-app-in-swift): In-App Purchases

Welcome to part 7 of my swift programming tutorial. In the previous parts we've created [sprites, added movement, enemies with a follow behaviour, bullets & shooting](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-2), a [HUD](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-3-create-a-hud), [collision detection](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-4-collision-detection), [sound & particle effects](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-5-particles-and-sound) and a global leaderboard using [Game Center](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-6-game-center-integration). Today I'll show how to integrate the Apple Advertising Framework **iAD** : 

  * Enable iAd in iTunesConnect
  * Add a Banner Ad (at the bottom of the screen)
  * Add a Fullscreen Ad (after game over)



## **Let's start:**

###  1. Enable iAD support in iTunes Connect

You need a paid Apple Developer Account to execute the next steps. 

**Open [ iTunes Connect](https://itunesconnect.apple.com/) and navigate to the Agreements, Tax and Banking section:**

[![](/assets/wp-content/uploads/2015/02/Screen-2BShot-2B2015-02-05-2Bat-2B22.10.19-1.jpg)](/assets/wp-content/uploads/2015/02/Screen-2BShot-2B2015-02-05-2Bat-2B22.10.19-1.jpg)

### Request an iAd Agreement:

[![](/assets/wp-content/uploads/2015/02/iad.png)](/assets/wp-content/uploads/2015/02/iad.png)

### 2. Add a Banner Ad

In this section I'll show how to add a banner add at the bottom of the screen. As a starting point you can download the code from part 6 [here](https://github.com/stfnjstn/MySecondGame/releases/tag/v0.6).

[![](/assets/wp-content/uploads/2015/02/Screen-2BShot-2B2015-02-08-2Bat-2B16.46.48-1.jpg)](/assets/wp-content/uploads/2015/02/Screen-2BShot-2B2015-02-08-2Bat-2B16.46.48-1.jpg)

**Import the iAd framework and implement the ADBannerViewDelegate **protocol**:

```swift
import iAd

class GameViewController: UIViewController, ADBannerViewDelegate, GKGameCenterControllerDelegate, GameSceneDelegate {
```

**Add two properties to GameViewController to keep a reference to the banner object and the visibility state:**

```swift
// Properties for Banner Ad
var iAdBanner = ADBannerView()
var bannerVisible = false
```

**Add the code to initialise the banner at the end of viewDidAppear:**

```swift
override func viewDidAppear(animated: Bool) {
  super.viewDidAppear(animated)
  ...

  // Prepare banner Ad
  iAdBanner.frame = CGRectMake(0, self.view.frame.size.height, self.view.frame.width, 50)
  iAdBanner.delegate = self
  bannerVisible = false
}
```

**Implement the protocol method bannerViewDidLoadAd to move the banner on the screen, if an ad is loaded:**

```swift
// Show banner, if Ad is successfully loaded.
func bannerViewDidLoadAd(banner: ADBannerView!) {
  if(bannerVisible == false) {

    // Add banner Ad to the view
    if(iAdBanner.superview == nil) {
      self.view.addSubview(iAdBanner)
    }

    // Move banner into visible screen frame:
    UIView.beginAnimations("iAdBannerShow", context: nil)
    banner.frame = CGRectOffset(banner.frame, 0, -banner.frame.size.height)
    UIView.commitAnimations()
    bannerVisible = true
  }
}
```

**Implement the protocol method bannerView to remove the banner from screen, if an ad is not available:** **

```swift
// Hide banner, if Ad is not loaded.
func bannerView(banner: ADBannerView!, didFailToReceiveAdWithError error: NSError!) {
  if(bannerVisible == true) {
  
    // Move banner below screen frame:
    UIView.beginAnimations("iAdBannerHide", context: nil)
    banner.frame = CGRectOffset(banner.frame, 0, banner.frame.size.height)
    UIView.commitAnimations()
    bannerVisible = false
  }
}
```


### 3. Add a Fullscreen Ad

**Add this code to prepare a Fullscreen Ad at the end of viewDidAppear:** **

```swift
override func viewDidAppear(animated: Bool) {
  super.viewDidAppear(animated)
  ...

  // Prepare fullscreen Ad
  UIViewController.prepareInterstitialAds()
}
```

**Add a new method openAds to show a Action Sheet where the player can chose to open the Ad or play again:**

```swift
// Open a fullscreen Ad
func openAds(sender: AnyObject) {

  // Create an alert
  var alert = UIAlertController(title: "", message: "Play again?", preferredStyle: UIAlertControllerStyle.Alert)

  // Play again option
  alert.addAction(UIAlertAction(title: "Yes", style: UIAlertActionStyle.Default) { _ in
    self.scene!.gameOver = false
  })

  // Show fullscreen Ad option
  alert.addAction(UIAlertAction(title: "Watch Ad", style: UIAlertActionStyle.Default) { _ in
    self.interstitialPresentationPolicy = ADInterstitialPresentationPolicy.Manual
    self.requestInterstitialAdPresentation()
    self.scene!.gameOver = false
  })

  self.presentViewController(alert, animated: true, completion: nil)

  }
```

[![](/assets/wp-content/uploads/2015/02/Screen-2BShot-2B2015-02-08-2Bat-2B22.20.11.png)](/assets/wp-content/uploads/2015/02/Screen-2BShot-2B2015-02-08-2Bat-2B22.20.11.png)

**Add the call of the action sheet method in gameOver and gameCenterViewControllerDidFinish **

```swift
// Show game center leaderboard
func gameOver() {
  ...

  // Show leaderboard
  if GKLocalPlayer.localPlayer().authenticated == true {
    self.presentViewController(gcViewController, animated: true, completion: {
    })
  } else {
    // Show fullscreen Ad
    self.openAds(self)
  }
}

// Continue the game after GameCenter is closed
func gameCenterViewControllerDidFinish(gameCenterViewController: GKGameCenterViewController!) {
  gameCenterViewController.dismissViewControllerAnimated(true, completion: nil)

  // Show fullscreen Ad
  openAds(self)
}
```

[![](/assets/wp-content/uploads/2015/02/Screen-2BShot-2B2015-02-08-2Bat-2B22.20.56-1.jpg)](/assets/wp-content/uploads/2015/02/Screen-2BShot-2B2015-02-08-2Bat-2B22.20.56-1.jpg)

That's all for today. You can download the code from GitHub: [Part 7](https://github.com/stfnjstn/MySecondGame/releases/tag/v0.7) or the [latest version](https://github.com/stfnjstn/MySecondGame/tree/master). 

I've submitted this version to the Apple AppStore. In one of my next posts I'll show how to implement social media integration. If you want to get an idea what is coming: 

A more sophisticated game based on this tutorial series is available in the AppStore: 

[![](/assets/wp-content/uploads/2015/04/AppStore.png)](https://itunes.apple.com/us/app/yet-another-spaceshooter/id949662362?mt=8)

Cheers,    
Stefan

---
layout: post
permalink: /quick-tip-implement-fullscreen-interstitial-ads-for-ios-in-swift/
title: 'Quick Tip: Implement fullscreen / interstitial Ads for iOS in SWIFT'
seo_title: 'Quick Tip: Implement fullscreen (interstitial) Ads for iOS in SWIFT'
description: Usually you can play free games a certain time, till a fullscreen / interstitial
  Ad is shown. Implementing this requires only few lines of SWIFT code.
date: 2015-06-14 19:31:57 -0000
last_modified_at: 2020-05-27 16:40:56 -0000
publish: true
pin: false
categories:
- AdSense and Admob
- iOS
- SWIFT
tags: []
---
## How to implement an Interstitial Ad combined with a counter

Today I'll show how to implement a often used pattern in free games: Usually you can play free games a certain time, till a fullscreen ad is shown. For example after each third game over an ad is shown. Implementing this behaviour for the iOS platform requires only few lines of code in SWIFT.

For details how to subscribe for the Apple iAds program, please check my previous article about [iAD integration](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-7-iad-integration).

### 1. Create the sample project:

![iAD1](/assets/2015/06/iAD1.png)

![iAD2](/assets/2015/06/iAD2.png)

### 2. Create the sample program flow:

Add a new UIViewController class to your project and name it TargetViewController:

![iAD3](/assets/2015/06/iAD3-1.jpg)

![iAD4](/assets/2015/06/iAD4.png)

![iAD5](/assets/2015/06/iAD5.png)

![iAD6](/assets/2015/06/iAD6-1.jpg)

Place a new UIViewController on the Storyboard and add a button to each ViewController

![iAd7](/assets/2015/06/iAd7.png)

Add constraints to the buttons to centre them on the screen for each form factor, orientation and resolution:

![iAD8](/assets/2015/06/iAD8.png)

Change type of the new view controller to TargetViewController:

![iAD9](/assets/2015/06/iAD9.png)

Add a unwindFromTargetViewController method to your ViewController class:

```swift
import UIKit

class ViewController: UIViewController {
  override func viewDidLoad() {
    super.viewDidLoad()
    // Do any additional setup after loading the view, typically from a nib.
  }

  override func didReceiveMemoryWarning() {
    super.didReceiveMemoryWarning()
    // Dispose of any resources that can be recreated.
  }

  @IBAction func unwindFromTargetViewController(segue: UIStoryboardSegue) {

  }
}
```

**Now implement the navigation between the ViewControllers:** Control Drag the first button, move it to TargetViewController and create a segue to implement the navigation from ViewController to TargetViewController:

![iAD10](/assets/2015/06/iAD10.png)

Control Drag the button in TargetViewController and move the mouse pointer to the Exit box of ViewController:

![iAD11](/assets/2015/06/iAD11-1.jpg)

Select the unwindFromTargetViewController method:

![iAD12](/assets/2015/06/iAD12.png)

As a result you see a segue under each ViewController:

![iAD13](/assets/2015/06/iAD13.png)

More on segues in my previous tutorial about [View Navigation](/howto-add-view-controllers-to-the-game-storyboard-and-use-segues-to-navigate-between-them).

### 3. Implement the iAd Integration

If you start the project you can navigate from the start screen to the second screen and back. Now I'll implement the logic to show a fullscreen (interstitial) ad after each third navigation to the second screen.

#### Add the iAD framework to your project:

![iAD14](/assets/2015/06/iAD14-1.jpg)

#### Open ViewController.swift:

At the top import the iAD framework and define a global counter:

```swift
import UIKitimport iAd

var counter = 0
class ViewController: UIViewController {
  ```

Add this code to the viewDidLoad method to initialise the ads:

```swift
override func viewDidLoad() {
  super.viewDidLoad()
  // Initialize the Ad
  UIViewController.prepareInterstitialAds()
}
```

Implement the logic to open the ad after each third third navigation to the second screen inside of the prepareForSegue method:

```swift
override func prepareForSegue(segue: UIStoryboardSegue, sender: AnyObject?) {
  counter++
  if counter == 2 {
    counter = 0
    let destination = segue.destinationViewController as! UIViewController
    destination.interstitialPresentationPolicy = ADInterstitialPresentationPolicy.Automatic
  }
}
```

Thats all! Apple takes care about ads loading and error handling and decides, if the ad is ready to show. It can happen that no ad is shown. For example, if you click to fast in this sample project no new ad is available.

![iAD15](/assets/2015/06/iAD15-1.jpg)

You can download the sample code from my [GitHub repository](https://github.com/stfnjstn/iAdSample). That's all for today.  
  
Cheers,  
Stefan

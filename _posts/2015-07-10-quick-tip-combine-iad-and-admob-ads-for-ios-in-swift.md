---
layout: post
permalink: /quick-tip-combine-iad-and-admob-ads-for-ios-in-swift/
title: 'Quick Tip: Combine iAd and AdMob Ads for iOS in SWIFT'
seo_title: 'Quick Tip: Combine iAd and AdMob Ads for iOS in SWIFT'
description: This tutorial shows how to use iAd and AdMob Ads in the same app for
  iOS in SWIFT to get a better fill rate.
date: 2015-07-10 14:46:29 -0000
last_modified_at: 2020-05-27 16:40:56 -0000
publish: true
pin: false
image:
  path: /assets/2015/07/Screen-Shot-2015-07-10-at-15.14.21-1.jpg
categories:
- AdSense and Admob
- iOS
- SWIFT
tags:
- AdMob
- AdSense
---
## Use iAd and AdMob ads in the same app

Today I'll show how to use iAd together with AdMob ads. If you use the interstitial ads provided by Apples iAd frequently, you might have seen that the fill rate is not always 100 percent:

[![AdMob tutorial](/assets/2015/07/Screen-Shot-2015-07-10-at-14.20.17.png)](/assets/2015/07/Screen-Shot-2015-07-10-at-14.20.17.png)

One reason could be that there was just not enough time to load the new content. This tutorial shows how to improve the fill rate by requesting a Google AdMob ad in parallel. Depending on the availability, the iAd or the AdMob ad will be shown.

#### Prerequisites for this tutorial:

  * You have a subscription for the Apple iAds program. For details please check my previous article about [iAD integration](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-7-iad-integration).
  * You are registered for the Google [AdMob](https://www.google.com/admob/) program
  * You have downloaded the Google [AdMob SDK for iOS](https://developers.google.com/admob/ios/download)



### 1. Let's create a sample project:

[![AdMob 1](/assets/2015/07/Screen-Shot-2015-07-10-at-14.28.16.png)](/assets/2015/07/Screen-Shot-2015-07-10-at-14.28.16.png)

[![AdMob 2](/assets/2015/07/Screen-Shot-2015-07-10-at-14.28.35.png)](/assets/2015/07/Screen-Shot-2015-07-10-at-14.28.35.png)

### 2. Ad the iAD framework to your project:

[![AdMob 3](/assets/2015/07/Screen-Shot-2015-07-08-at-21.57.041-1.jpg)](/assets/2015/07/Screen-Shot-2015-07-08-at-21.57.041-1.jpg)

[![AdMob 4](/assets/2015/07/Screen-Shot-2015-07-08-at-21.57.191.png)](/assets/2015/07/Screen-Shot-2015-07-08-at-21.57.191.png)

[![5](/assets/2015/07/Screen-Shot-2015-07-08-at-21.57.291.png)](/assets/2015/07/Screen-Shot-2015-07-08-at-21.57.291.png)

### 3. Ad the Google AdMob SDK to your project:

[![AdMob 6](/assets/2015/07/Screen-Shot-2015-07-10-at-14.33.12-1.jpg)](/assets/2015/07/Screen-Shot-2015-07-10-at-14.33.12-1.jpg)

[![AdMob 7](/assets/2015/07/Screen-Shot-2015-07-10-at-14.33.51-1.jpg)](/assets/2015/07/Screen-Shot-2015-07-10-at-14.33.51-1.jpg)

[![AdMob 8](/assets/2015/07/Screen-Shot-2015-07-10-at-14.34.03.png)](/assets/2015/07/Screen-Shot-2015-07-10-at-14.34.03.png)

### 4. Create the UI:

#### Open the storyboard and add a button to the screen:

[![AdMob 9](/assets/2015/07/Screen-Shot-2015-07-10-at-14.36.02.png)](/assets/2015/07/Screen-Shot-2015-07-10-at-14.36.02.png)

#### Use Autolayout to center the button on the screen:

[![AdMob 10](/assets/2015/07/Screen-Shot-2015-07-10-at-14.36.21.png)](/assets/2015/07/Screen-Shot-2015-07-10-at-14.36.21.png)

#### Create an IBAction method to handle touch events for the button:

[![AdMob 11](/assets/2015/07/Screen-Shot-2015-07-10-at-14.41.05.png)](/assets/2015/07/Screen-Shot-2015-07-10-at-14.41.05.png)

### 5. Create the AdHelper class

[![AdMob 12](/assets/2015/07/Screen-Shot-2015-07-10-at-14.51.05-1.jpg)](/assets/2015/07/Screen-Shot-2015-07-10-at-14.51.05-1.jpg)

[![AdMob 13](/assets/2015/07/Screen-Shot-2015-07-10-at-14.51.14.png)](/assets/2015/07/Screen-Shot-2015-07-10-at-14.51.14.png)

[![AdMob 14](/assets/2015/07/Screen-Shot-2015-07-10-at-14.51.26.png)](/assets/2015/07/Screen-Shot-2015-07-10-at-14.51.26.png)

#### Paste this code snippet into the newly created file:

```swift
// Helper class to show iAd and Google AdMob interstitial ads. Default is the iAd.
// If a new iAD add is not available an Google AdMob ad will be shown

import UIKit
import iAd
import GoogleMobileAds

class AdHelper: NSObject {
  private var iterationsTillPresentAd = 0 // Can be used to show an ad only after a fixed number of iterations
  private var adMobKey = "" // Stores the key provided by google
  private var counter = 0
  private var adMobInterstitial: GADInterstitial!

  // Initialize iAd and AdMob interstitials ads
  init(presentingViewController: UIViewController, googleAdMobKey: String, iterationsTillPresentInterstitialAd: Int) {
    self.iterationsTillPresentAd = iterationsTillPresentInterstitialAd
    self.adMobKey = googleAdMobKey
    self.adMobInterstitial = GADInterstitial(adUnitID: self.adMobKey)
    presentingViewController.interstitialPresentationPolicy = ADInterstitialPresentationPolicy.Manual 
  }

  // Present the interstitial ads
  func showAds(presentingViewController: UIViewController) {
    // Check if ad should be shown
    counter++
    if counter >= iterationsTillPresentAd {
      // Try if iAd ad is available
      if presentingViewController.requestInterstitialAdPresentation() {
        counter = 0
        presentingViewController.interstitialPresentationPolicy = ADInterstitialPresentationPolicy.None

        // The ad was used. Prefetch the next one
        preloadIAdInterstitial(presentingViewController)
        // Try if the AdMob is available
      } else {
        if adMobInterstitial == nil {
          // In case the disableAd was called
          adMobInterstitial = GADInterstitial(adUnitID: self.adMobKey)
      } else {
          // Present the AdMob ad, if available
          if (self.adMobInterstitial.isReady) {
            counter = 0
            adMobInterstitial!.presentFromRootViewController(presentingViewController)
            adMobInterstitial = GADInterstitial(adUnitID: self.adMobKey)
          }
        }

        // Prefetch the next ads
        preloadIAdInterstitial(presentingViewController)
        preloadAdMobInterstitial()
      }
    }
  }

  // Disable ads
  func disableAd(presentingViewController: UIViewController) {
    presentingViewController.interstitialPresentationPolicy = ADInterstitialPresentationPolicy.None
    adMobInterstitial = nil
  }

  // Prefetch AdMob ads
  private func preloadAdMobInterstitial() {
    var request = GADRequest()
    request.testDevices = ["kGADSimulatorID"] // Needed to show Ads in the simulator
    self.adMobInterstitial.loadRequest(request)
  }

  // Prefetch iAd ads
  private func preloadIAdInterstitial(presentingViewController: UIViewController) {
    presentingViewController.interstitialPresentationPolicy = ADInterstitialPresentationPolicy.Manual
    UIViewController.prepareInterstitialAds()
  }
}
```

### 6. Call the AdHelper class

#### Open ViewController.swift:

#### [![AdMob 11](/assets/2015/07/Screen-Shot-2015-07-10-at-15.01.41-1.jpg)](/assets/2015/07/Screen-Shot-2015-07-10-at-15.01.41-1.jpg)

#### Add a property which hold the instance of AdHelper and initialise it in the ViewDidLoad method:

```swift
import UIKit

class ViewController: UIViewController {
  var adHelper: AdHelper!

  override func viewDidLoad() {
    super.viewDidLoad()
    adHelper = AdHelper(presentingViewController: self, googleAdMobKey: "PASTE YOU ADMOB ID HERE", iterationsTillPresentInterstitialAd: 1)
  }
```

#### Enter the code to call the ad each time the button is pressed:

```swift
@IBAction func showAd(sender: AnyObject) {
  adHelper.showAds(self)
}
```

#### Now you can test this on a device:

[![AdMob 14](/assets/2015/07/Screen-Shot-2015-07-10-at-15.14.21-1.jpg)](/assets/2015/07/Screen-Shot-2015-07-10-at-15.14.21-1.jpg)

That's all for today. You can download the Sample from my GitHub [repository](https://github.com/stfnjstn/iAdAdMobDemo). Further details about the Google AdMob SDK can be found [here](https://developers.google.com/admob/ios/interstitial).

Cheers,  
Stefan

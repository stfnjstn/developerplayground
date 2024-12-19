---
layout: post
permalink: /quick-tip-integrate-iad-banner-ads-to-your-ios-app-with-two-lines-of-code/
title: 'Quick Tip: Integrate iAd banners in your iOS App with two lines of code'
seo_title: 'Quick Tip: Integrate iAd banners in your iOS App with two lines of code'
description: Most tutorials explain the complex version how to integrate iAd banners
  with the ADBannerViewDelegate protocol. Here is a two lines of SWIFT code solution
date: 2015-07-08 20:40:37 -0000
last_modified_at: 2020-05-27 16:40:56 -0000
publish: true
pin: false
image:
  path: /assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-22.01.17-1.jpg
categories:
- iOS
- SWIFT
tags:
- iAD
---
## The easiest way to add iAD banners to your app

Today I'll show a very simple way to integrate an ad banner to your iOS app. Most tutorials (including mine) explain the complex way by implementing the ADBannerViewDelegate protocol. If you don't care about error handling, animations, positioning or the maximum number of allowed banner instances (10!): There is a much easier way which requires only two lines of code in SWIFT to integrate iAD.

For details how to subscribe for the Apple iAds program, please check my previous article about [iAD integration](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-7-iad-integration " iAD integration").

### 1. Create the sample project:

[![iAd Tutorial](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-21.55.35.png)](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-21.55.35.png) [![iAd Tutorial](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-21.55.52.png)](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-21.55.52.png)

### 2. Ad the iAD framework to your project:

[![iAd Tutorial](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-21.57.04-1.jpg)](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-21.57.04-1.jpg) [![iAd Tutorial](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-21.57.19.png)](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-21.57.19.png) [![iAd Tutorial](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-21.57.29.png)](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-21.57.29.png)

### 3. Add these two lines of code to your ViewController class:

```swift
import UIKit
import iAd

class ViewController: UIViewController {
  override func viewDidLoad() {
    super.viewDidLoad()
    self.canDisplayBannerAds = true
  }
}
```

Thats all! Apple takes care about ads loading and error handling and decides, if the ad is ready to show. Apple also handles orientation changes and the different sizes for iPhone and iPad. [![Integrate iAd](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-22.01.17-1.jpg)](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-22.01.17-1.jpg) [![iAd Tutorial](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-22.01.36-1.jpg)](/assets/wp-content/uploads/2015/07/Screen-Shot-2015-07-08-at-22.01.36-1.jpg)

That's all for today.

Cheers,  
Stefan

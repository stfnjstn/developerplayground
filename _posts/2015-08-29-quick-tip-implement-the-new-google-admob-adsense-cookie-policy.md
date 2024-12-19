---
layout: post
permalink: /quick-tip-implement-the-new-google-admob-adsense-cookie-policy/
title: 'Quick Tip: Implement the new Google AdMob / AdSense Cookie Policy'
seo_title: Implement the new Google Cookie Policy for AdSense and AdMob
description: This SWIFT tutorial shows how to implement the new Google Cookie policy
  for AdMob or AdSense usage in your apps.
date: 2015-08-29 17:31:08 -0000
last_modified_at: 2020-05-27 16:40:56 -0000
publish: true
pin: false
image:
  path: /assets/wp-content/uploads/2015/08/iOS-Simulator-Screen-Shot-29-Aug-2015-19.02.15.png
categories:
- AdSense and Admob
- iOS
- SWIFT
tags:
- AdMob
- AdSense
---
In the last days Google sent out emails to App developers which uses their AdSense and AdMob frameworks explaining the new Google Cookie Policy. Google urges them to inform their users about the usage of the advertising cookies:

**From Google:**

> European laws require that digital publishers give visitors to their sites and apps information about their use of cookies and other forms of local storage. In many cases these laws also require that consent be obtained.

In this tutorial I'll show how you can implement an information alert about the cookie usage in SWIFT. The basic idea is to detect, if the app is started the first time:

  * If yes show an alert with a message about the cookie usage.
  * After clicking _OK_ store a key in NSUserDefault.
  * Next time the application is started, this key will be found and therefore no alert will be shown.

**IMPORTANT:** I'm not a lawyer. So no guarantees. You have to decide on your own if this is sufficient.

[![Google Cookie Policy](/assets/wp-content/uploads/2015/08/iOS-Simulator-Screen-Shot-29-Aug-2015-19.02.15.png)](/assets/wp-content/uploads/2015/08/iOS-Simulator-Screen-Shot-29-Aug-2015-19.02.15.png)

The Code snippet for showing the AdMob Cookie usage is simple:

```swift
// AdMob Cookie handling:
// Warning: I'm not a lawyer. You have to decide on your own, if this is sufficient
// Google gives more hints on: [http://www.cookiechoices.org](http://www.cookiechoices.org/)

let adMobTitle = "Cookie usage:"
let adMobCookieText = "We use device identifiers to personalise content and ads, to provide social media features and to analyse our traffic. We also share such identifiers and other information from your device with our social media, advertising and analytics partners."
let userDefaults : NSUserDefaults = NSUserDefaults.standardUserDefaults()
if !userDefaults.boolForKey("termsAccepted") {
  var alert = UIAlertController(title: adMobTitle, message: adMobCookieText, preferredStyle: UIAlertControllerStyle.Alert)
  alert.addAction(UIAlertAction(title: "OK", style: UIAlertActionStyle.Default) { _ in
    userDefaults.setBool(true, forKey: "termsAccepted")
  })
  presentingViewController.presentViewController(alert, animated: true, completion: nil)
}
```

I've also updated the sample code in my [GitHub repository](https://github.com/stfnjstn/iAdAdMobDemo) from the [iAd & AdMob tutorial.](/how-to-implement-a-space-shooter-with-spritekit-and-swift-part-6-game-center-integration70)

Google gives more details and shows how to implement this in ObjectiveC at [http://www.cookiechoices.org](http://www.cookiechoices.org/). Further details about the Google AdMob SDK can be found [here](https://developers.google.com/admob/ios/interstitial).

That's all for today.

Cheers,  
Stefan

[![AppStore Stefan Josten](/assets/wp-content/uploads/2015/11/AppStore1.png)](https://itunes.apple.com/us/app/yet-another-watch-puzzle-game/id997514879?ls=1&mt=8)

 

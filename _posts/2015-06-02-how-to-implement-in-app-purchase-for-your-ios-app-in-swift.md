---
layout: post
permalink: /how-to-implement-in-app-purchase-for-your-ios-app-in-swift/
title: In-App Purchases
seo_title: In-App Purchases for your iOS App in SWIFT
description: Tutorial about the implementation of In-App Purchases in SWIFT for the
  iOS platform.
date: 2015-06-02 21:31:22 -0000
last_modified_at: 2020-05-27 16:40:55 -0000
publish: true
pin: false
categories:
- In-App Purchase
- iOS
- SpriteKit
tags:
- In-App Purchase
---
### In-App Purchases: How to implement a space shooter with SpriteKit and SWIFT - Part 8

[![](/assets/wp-content/uploads/2014/11/AppStore3.png)](https://itunes.apple.com/us/app/yet-another-spaceshooter/id949662362?mt=8)

 

#### 

#### Tutorial Overview: How to implement a space shooter with SpriteKit and SWIFT

  * [Part 1](https://developerplayground.net/?p=14): Initial project setup, sprite creation and movement using SKAction and SKConstraint
  * [Part 2](https://developerplayground.net/?p=13): Adding enemies, bullets and shooting with SKAction and SKConstraint
  * [Part 3](https://developerplayground.net/?p=12): Adding a HUD with SKLabelNode and SKSpriteNode
  * [Part 4](https://developerplayground.net/?p=11): Adding basic game logic and collision detection
  * [Part 5](https://developerplayground.net/?p=10): Adding particles and sound 
  * [Part 6](https://developerplayground.net/?p=9): GameCenter integration
  * [Part 7](https://developerplayground.net/?p=8): iAd integration
  * [Part 8](https://developerplayground.net/?p=5): In-App Purchases



### Adding In-App Purchases:

Welcome to part 8 of my swift programming tutorial. Today I'll show how to implement **In-App Purchases:**

  * Create In-App Purchases in iTunesConnect
  * Implement In-App Purchases
  * Test and upload to iTunesConnect



[![InApp01](/assets/wp-content/uploads/2015/04/InApp01-1-300x179.jpg)](/assets/wp-content/uploads/2015/04/InApp01-1.jpg) ![InApp02](/assets/wp-content/uploads/2015/04/InApp02-300x166.png)

 

As a starting point you can download the sample project from my GitHub [repository](https://github.com/stfnjstn/MySecondGame/releases/tag/v0.7). 

## Let's start:

### 1\. Create In-App Purchases in iTunes Connect

You need a paid Apple Developer Account to execute the next steps. For details about the process to upload Apps to iTunes Connect check tutorial [part 6](https://developerplayground.net/?p=9).

Browse to [iTunes Connect](https://itunesconnect.apple.com) and open your App: [![InApp2](/assets/wp-content/uploads/2015/04/InApp2-1-300x149.jpg)](/assets/wp-content/uploads/2015/04/InApp2-1.jpg) Choose **In-App Purchases** and click on **Create New** : [![InApp3](/assets/wp-content/uploads/2015/04/InApp3-300x67.png)](/assets/wp-content/uploads/2015/04/InApp3.png) You see several different types of possible purchases. In this tutorial I'll show a '**Consumable** ' and a '**Non-Consumable** ' purchase. [![InApp4](/assets/wp-content/uploads/2015/04/InApp4-300x235.png)](/assets/wp-content/uploads/2015/04/InApp4.png) Create the **Consumable** purchase: [![InApp5](/assets/wp-content/uploads/2015/04/InApp5-300x46.png)](/assets/wp-content/uploads/2015/04/InApp5.png) Enter **Reference Name** , **Product ID** and **Price Tier** : [![InApp6](/assets/wp-content/uploads/2015/04/InApp6-300x174.png)](/assets/wp-content/uploads/2015/04/InApp6.png) Add **Display Name** and **Description** at least for one language: [![InApp7](/assets/wp-content/uploads/2015/04/InApp7-300x98.png)](/assets/wp-content/uploads/2015/04/InApp7.png) Additionally a screenshot is needed for the review team: [![InApp8](/assets/wp-content/uploads/2015/04/InApp8-300x74.png)](/assets/wp-content/uploads/2015/04/InApp8.png) Now do the same for the **Non-Consumable** purchase: [![InApp9](/assets/wp-content/uploads/2015/04/InApp9-300x43.png)](/assets/wp-content/uploads/2015/04/InApp9.png) [![InApp14](/assets/wp-content/uploads/2015/04/InApp14-300x164.png)](/assets/wp-content/uploads/2015/04/InApp14.png) The final result should look like this: [![InApp15](/assets/wp-content/uploads/2015/04/InApp15-300x173.png)](/assets/wp-content/uploads/2015/04/InApp15.png)

### 2\. Implement In-App Purchases

Open your project in XCode (sample project is available [here](https://github.com/stfnjstn/MySecondGame/releases/tag/v0.7)), navigate to the **Capabilities** configuration page and enable **In-App Purchases** : [![InApp12](/assets/wp-content/uploads/2015/04/InApp12-300x124.png)](/assets/wp-content/uploads/2015/04/InApp12.png) Xcode will include the **StoreKit** framework and add the **In-App Purchase** entitlement automatically.

#### 2.1. Add a button to trigger the purchases:

Open the **createHUD** method in **GameScene.swift** and add this code snippet to add a '$$$' button to the header: [![InApp13](/assets/wp-content/uploads/2015/04/InApp13.png)](/assets/wp-content/uploads/2015/04/InApp13.png)

func createHUD() {

...

// Add a $ Button for In-App Purchases:

var purchaseButton = SKLabelNode()

purchaseButton.position = CGPointMake(hud.size.width/1.5, 1)

purchaseButton.text="$$$"

purchaseButton.fontSize=hud.size.height

purchaseButton.horizontalAlignmentMode = SKLabelHorizontalAlignmentMode.Center

purchaseButton.name="PurchaseButton"

Add these two lines to **touchesBegan** to call **inAppPurchase** :

override func touchesBegan(touches: Set<NSObject>, withEvent event: UIEvent) {

/* Called when a touch begins */

for touch in (touches as! Set<UITouch>) {

var location = touch.locationInNode(self)

var node = self.nodeAtPoint(location)

if (node.name == "PauseButton") || (node.name == "PauseButtonContainer") {

showPauseAlert()

} else if (node.name == "PurchaseButton") {

inAppPurchase()

} else {

...

Add an empty inAppPurchase method:

func inAppPurchase() {

}

#### 2.2. Implement Puchase

All changes will be done in GameScene.swift. Import the StoreKit framework: import StoreKit Add the StoreKit protocols:

class GameScene: SKScene, SKPhysicsContactDelegatee, SKPaymentTransactionObserver, SKProductsRequestDelegate {

Add these lines at the end of the **didMoveToView** method to initialise the purchase objects and to check if the new feature is already purchased:

// In-App Purchase

initInAppPurchases()

checkAndActivateGreenShip()

I've documented the missing methods in the code itself:

// ---------------------------------

// ---- Handle In-App Purchases ----

// ---------------------------------

private var request : SKProductsRequest!

private var products : [SKProduct] = [] // List of available purchases

private var greenShipPurchased = false // Used to enable/disable the 'green ship' feature

// Open a menu with the available purchases

func inAppPurchase() {

var alert = UIAlertController(title: "In App Purchases", message: "", preferredStyle: UIAlertControllerStyle.Alert)

self.gamePaused = true

// Add an alert action for each available product

for (var i = 0; i < products.count; i++) {

var currentProduct = products[i]

if !(currentProduct.productIdentifier == "MySecondGameGreenShip" && greenShipPurchased) {

// Get the localized price

let numberFormatter = NSNumberFormatter()

numberFormatter.numberStyle = .CurrencyStyle

numberFormatter.locale = currentProduct.priceLocale

// Add the alert action

alert.addAction(UIAlertAction(title: currentProduct.localizedTitle \+ " " \+ numberFormatter.stringFromNumber(currentProduct.price)!, style: UIAlertActionStyle.Default) { _ in

// Perform the purchase

self.buyProduct(currentProduct)

self.gamePaused = false

})

}

}

// Offer the restore option only if purchase info is not available

if(greenShipPurchased == false) {

alert.addAction(UIAlertAction(title: "Restore", style: UIAlertActionStyle.Default) { _ in

self.restorePurchasedProducts()

self.gamePaused = false

})

}

alert.addAction(UIAlertAction(title: "Cancel", style: UIAlertActionStyle.Default) { _ in

self.gamePaused = false

})

// Show the alert

self.view?.window?.rootViewController?.presentViewController(alert, animated: true, completion: nil)

}

// Initialize the App Purchases

func initInAppPurchases() {

SKPaymentQueue.defaultQueue().addTransactionObserver(self)

// Get the list of possible purchases

if self.request == nil {

self.request = SKProductsRequest(productIdentifiers: Set(["MySecondGameGreenShip","MySecondGameDonate"]))

self.request.delegate = self

self.request.start()

}

}

// Request a purchase

func buyProduct(product: SKProduct) {

let payment = SKPayment(product: product)

SKPaymentQueue.defaultQueue().addPayment(payment)

}

// Restore purchases

func restorePurchasedProducts() {

SKPaymentQueue.defaultQueue().restoreCompletedTransactions()

}

// StoreKit protocoll method. Called when the AppStore responds

func productsRequest(request: SKProductsRequest!, didReceiveResponse response: SKProductsResponse!) {

self.products = response.products as! [SKProduct]

self.request = nil

}

// StoreKit protocoll method. Called when an error happens in the communication with the AppStore

func request(request: SKRequest!, didFailWithError error: NSError!) {

println(error)

self.request = nil

}

// StoreKit protocoll method. Called after the purchase

func paymentQueue(queue: SKPaymentQueue!, updatedTransactions transactions: [AnyObject]!) {

for transaction in transactions as! [SKPaymentTransaction] {

switch (transaction.transactionState) {

case .Purchased:

if transaction.payment.productIdentifier == "MySecondGameGreenShip" {

handleGreenShipPurchased()

}

queue.finishTransaction(transaction)

case .Restored:

if transaction.payment.productIdentifier == "MySecondGameGreenShip" {

handleGreenShipPurchased()

}

queue.finishTransaction(transaction)

case .Failed:

println("Payment Error: %@", transaction.error)

queue.finishTransaction(transaction)

default:

println("Transaction State: %@", transaction.transactionState)

}

}

}

// Called after the purchase to provide the 'green ship' feature

func handleGreenShipPurchased() {

greenShipPurchased = true

checkAndActivateGreenShip()

// persist the purchase locally

NSUserDefaults.standardUserDefaults().setBool(true, forKey: "MySecondGameGreenShip")

}

// Called after applicattion start to check if the 'green ship' feature was purchased

func checkAndActivateGreenShip() {

if NSUserDefaults.standardUserDefaults().boolForKey("MySecondGameGreenShip") {

greenShipPurchased = true

heroSprite.color = UIColor.greenColor()

heroSprite.colorBlendFactor=0.8

}

}

### Test and upload to iTunes Connect

You need a Sandbox Test User to test the purchases. I've described the steps to create one in [part 6](https://developerplayground.net/?p=9). [![InApp16](/assets/wp-content/uploads/2015/04/InApp16-300x149.png)](/assets/wp-content/uploads/2015/04/InApp16.png)

Testing is only possible on a real device. If you try a purchase in the simulator, you'll receive an error message: AppStore is not available. And don't forget to set the checkmarks on your purchases to include them to your them to your application bundle, before submitting a new version in iTunesConnect. 

That's all for today. The SourceCode of this tutorial is available at [GitHub](https://github.com/stfnjstn/MySecondGame/releases/tag/v0.8). To see **In-App Purchase** in action you can download my free [game](https://itunes.apple.com/us/app/yet-another-spaceshooter/id949662362?mt=8) in the AppStore. The **In-App Purchase** update will be released in the next days.

![](/assets/wp-content/uploads/2015/04/AppStore.png)

Cheers,   
Stefan
---
layout: post
permalink: /how-to-add-social-media-integration-to-your-ios-app/
title: How to add Social Media Integration to your iOS App
seo_title: How to add Social Media Integration to your iOS App
description: 'Tutorial: Implement social media integration for Facebook and Twitter,
  Email integration and embed an AppStore link to offer an easy way to rate an app.'
date: 2015-03-04 19:54:00 -0000
last_modified_at: 2020-05-27 16:40:54 -0000
publish: true
pin: false
categories:
- iOS
- Social Media
- SWIFT
tags:
- Facebook
- social media
- twitter
---
Welcome to my new SWIFT tutorial. Today I'll show you how to implement social media integration for Facebook and Twitter. Additionally I'll explain Email integration and how to embed a direct AppStore link to provide a convenient way for players to rate an app.

My latest [game](https://itunes.apple.com/us/app/yet-another-spaceshooter/id949662362?mt=8) in the AppStore contains a sample:

[![](/assets/wp-content/uploads/2015/04/IMG_8919.png)](https://itunes.apple.com/us/app/yet-another-spaceshooter/id949662362?mt=8)

The four buttons at the bottom of the screen trigger the social actions:

[![](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-02-26-2Bat-2B23.12.45.png)](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-02-26-2Bat-2B23.12.45.png)

### 1. Create a sample project:

Start XCode and create a new Single View Application:

[![](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.32.21.png)](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.32.21.png)

[![](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.32.38.png)](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.32.38.png)

Open the Main.storyboard file and add four buttons to the ViewController:

[![](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.33.34.png)](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.33.34.png)

For a proper layout on all form factors and orientations add the needed auto layout constraints:

  * Select the four buttons
  * Press the Pin button
  * Enter in the spacing to nearest neighbour section 20 to the bottom and 10 to the right

[![](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.34.55.png)](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.34.55.png)

XCode shows a warning, that the current layout does not match the constraints (the yellow lines). To fix this click the Resolve Auto Layout Issues button and choose Update Frames:

[![](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.35.11.png)](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.35.11. png)

The result should look like this:

[![](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.35.22.png)](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.35.22.png)

[![](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.36.22.png)](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B20.36.22.png)

Change the background colour of the view to black:

[![](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-03-2Bat-2B22.32.43.png)](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-03-2Bat-2B22.32.43.png)

Add an IBAction method for every button (Select CTRL, press mouse and move the mouse pointer to the view controller file)

[![](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B23.12.52.png)](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-02-2Bat-2B23.12.52.png)

The ViewController.swift file should look like this:

```swift
import UIKit

class ViewController: UIViewController {
  override func viewDidLoad() {

    super.viewDidLoad()
    // Do any additional setup after loading the view, typically from a nib.
  }

  @IBAction func handleAppStore(sender: AnyObject) {

  }

  @IBAction func handleFacebook(sender: AnyObject) {

  }

  @IBAction func handleTwitter(sender: AnyObject) {

  }

  @IBAction func handleMail(sender: AnyObject) {

  }
}
```

Add an image to image.assets which can be attached to the tweets, posts ands mail.

[![](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-04-2Bat-2B20.36.33-1.jpg)](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-03-04-2Bat-2B20.36.33-1.jpg)

### 2. Implement AppStore Integration

[![](/assets/wp-content/uploads/2015/03/IMG_8941-1.jpg)](/assets/wp-content/uploads/2015/03/IMG_8941-1.jpg)

Implement the handleAppStore method. Show an alert where the user can choose to navigate to the AppStore:

```swift
@IBAction func handleAppStore(sender: AnyObject) {
  let alert = UIAlertController(title: "Rate", message: "Rate my App", preferredStyle: UIAlertControllerStyle.Alert)
  alert.addAction(UIAlertAction(title: "Rate", style: UIAlertActionStyle.Default) { _ in
    // Open App in AppStore
    let iLink = "https://itunes.apple.com/us/app/yet-another-spaceshooter/id949662362?mt=8"
    UIApplication.sharedApplication().openURL(NSURL(string: iLink)!)
  })
  alert.addAction(UIAlertAction(title: "Cancel", style: UIAlertActionStyle.Default, handler: nil))
  self.presentViewController(alert, animated: true, completion: nil)
}
```

[![](/assets/wp-content/uploads/2015/03/IMG_8942-1.jpg)](/assets/wp-content/uploads/2015/03/IMG_8942-1.jpg)

### 3. Implement Mail Integration

[![](/assets/wp-content/uploads/2015/03/IMG_8948-1.jpg)](/assets/wp-content/uploads/2015/03/IMG_8948-1.jpg)

Import MessageUI and add the MFMailComposeViewControllerDelegate to the class definition:

```swift
import MessageUI
class ViewController: UIViewController, MFMailComposeViewControllerDelegate {
```

Implement the handleMail and mailComposeController methods:

```swift
@IBAction func handleMail(sender: AnyObject) {
  // Check if Mail is available
  if(MFMailComposeViewController.canSendMail()){
    // Create the mail message
    var mail = MFMailComposeViewController()
    mail.mailComposeDelegate = self
    mail.setSubject("New App")
    mail.setMessageBody("I want to share this App: ", isHTML: false)

    // Attach the image
    let imageData = UIImagePNGRepresentation(UIImage(named: "shareImage"))
    mail.addAttachmentData(imageData, mimeType: "image/png", fileName: "Image")
    self.presentViewController(mail, animated: true, completion: nil)
  } else {
    // Mail not available. Show a warning
    let alert = UIAlertController(title: "Email", message: "Email not available", preferredStyle: UIAlertControllerStyle.Alert)
    alert.addAction(UIAlertAction(title: "OK", style: UIAlertActionStyle.Default, handler: nil))
  self.presentViewController(alert, animated: true, completion: nil)
  }
}

// Required by interface MFMailComposeViewControllerDelegate
func mailComposeController(controller: MFMailComposeViewController!, didFinishWithResult result: MFMailComposeResult, error: NSError!) {
  // Close the mail dialog
  self.dismissViewControllerAnimated(true, completion: nil)
}
```

### 4. Implement Twitter Integration

[![](/assets/wp-content/uploads/2015/03/IMG_8940-1.jpg)](/assets/wp-content/uploads/2015/03/IMG_8940-1.jpg)

Import Social:

```swift
import Social
```

Implement the handleTwitter method:

```swift
@IBAction func handleTwitter(sender: AnyObject) {
  // Check if Twitter is available
  if(SLComposeViewController.isAvailableForServiceType(SLServiceTypeTwitter)) {
    // Create the tweet
    let tweet = SLComposeViewController(forServiceType: SLServiceTypeTwitter)
    tweet.setInitialText("I want to share this App: ")
    tweet.addImage(UIImage(named: "shareImage"))
    self.presentViewController(tweet, animated: true, completion: nil)
  } else {
    // Twitter not available. Show a warning
    let alert = UIAlertController(title: "Twitter", message: "Twitter not available", preferredStyle: UIAlertControllerStyle.Alert)
    alert.addAction(UIAlertAction(title: "OK", style: UIAlertActionStyle.Default, handler: nil))
    self.presentViewController(alert, animated: true, completion: nil)
  }
}
```

### 5. Implement Facebook Integration

Implement the handleFacebook method:

```swift
@IBAction func handleFacebook(sender: AnyObject) {
  // Check if Facebook is available
  if (SLComposeViewController.isAvailableForServiceType(SLServiceTypeFacebook)) {
    // Create the post
    let post = SLComposeViewController(forServiceType: (SLServiceTypeFacebook))
    post.setInitialText("I want to share this App: ")
    post.addImage(UIImage(named: "shareImage"))
    self.presentViewController(post, animated: true, completion: nil)
  } else {
    // Facebook not available. Show a warning
    let alert = UIAlertController(title: "Facebook", message: "Facebook not available", preferredStyle: UIAlertControllerStyle.Alert)
    alert.addAction(UIAlertAction(title: "OK", style: UIAlertActionStyle.Default, handler: nil))
    self.presentViewController(alert, animated: true, completion: nil)
  }
}
```

Instead of the text you should show icons. I cannot add them to the SourceCode because of copyright reasons. You can download them from Facebook and Twitter homepage. [![](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-02-26-2Bat-2B23.09.39-1.jpg)](/assets/wp-content/uploads/2015/03/Screen-2BShot-2B2015-02-26-2Bat-2B23.09.39-1.jpg)

That's all for today. The SourceCode of this tutorial is available at [GitHub](https://github.com/stfnjstn/SocialMediaSample). For my next post I'm planning something about In App Purchase. To see the social media integration in action you can download my free game in the AppStore:

[![](/assets/wp-content/uploads/2015/04/AppStore.png)](https://itunes.apple.com/us/app/yet-another-spaceshooter/id949662362?mt=8)

Cheers,    
Stefan 

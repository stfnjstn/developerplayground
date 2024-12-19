---
layout: post
permalink: /howto-add-view-controllers-to-the-game-storyboard-and-use-segues-to-navigate-between-them/
title: 'HowTo: Add View Controllers to the game storyboard and use segues to navigate
  between them'
seo_title: iOS View Controllers, Segues and Storyboards
description: iOS game development tutorial, viewcontroller segues, storyboard, game
  flow, iOS, objective c, xcode, tutorial, view controller
date: 2014-02-19 22:47:00 -0000
last_modified_at: 2020-05-27 16:40:54 -0000
publish: true
pin: false
categories:
- iOS
- ObjectiveC
- Storyboard
- UIKit
tags: []
---
### Welcome to Part 2 of my blog series about game development: View Controller

Today I'm creating the basic game infrastructure, not the game itself. If you haven't completed [part 1](/howto-design-for-depth-creating-a-start-screen-with-parallax-animations-using-ios-7-motion-effects), you can [download the project from GitHub (version v0.1](https://github.com/stfnjstn/MyFirstGame/releases/tag/v0.1)).

#### Basic screens needed for the game:

[![](/assets/wp-content/uploads/2014/02/ViewControllers.jpg)](/assets/wp-content/uploads/2014/02/ViewControllers1.jpg)

  * Start Screen: Main menue
  * About Screen: Information about the developer of the game, website, ...
  * Settings Screen: Choose settings like Sound on/off, ...
  * Play Screen: The Game
  * AddHighScoreScreen: Add a new highscore entry
  * Highscore: List of the highscores

[![](/assets/wp-content/uploads/2014/02/ViewControllers2-1.jpg)](/assets/wp-content/uploads/2014/02/ViewControllers2-1.jpg)

#### Reusing the code for the parallax effect

Before we create the corresponding view controllers take a step back and think about the two functions we've added to our StartScreenViewController to perform the parallax effect in [part 1](/howto-design-for-depth-creating-a-start-screen-with-parallax-animations-using-ios-7-motion-effects) of this blog series:

```objectivec
-(void)assignBackgroundParallaxBehavior:(UIView*) view
-(void)assignForegroundParallaxBehavior:(NSArray*) view
```

To avoid code duplication I'll create a new helper class: UITools 

[![](/assets/wp-content/uploads/2014/02/ViewControllers3-1.jpg)](/assets/wp-content/uploads/2014/02/ViewControllers3-1.jpg)

Add the declarationof the functions to UITools.m:
```objectivec
#import <Foundation/Foundation.h>

@interface UITools : NSObject
  +(void)assignBackgroundParallaxBehavior:(UIView*) view;
  +(void)assignForegroundParallaxBehavior:(NSArray*) view;
@end
```

I've declared the methods as static class methods ('+' instead of a '-'). That means they can be called directly without creating an instance of UITools.

After that copy the two functions from StartScreenViewController.m to UITools.m. Don't forget to change '-' to '+'.

We also need to import the new tools class in StartScreenViewController.m:
```objectivec
#import "UITools.h"
```
and change
```objectivec
[self assignBackgroundParallaxBehavior:self.backgroundView];

[self assignForegroundParallaxBehavior:self.foregroundViews];
```
to 
```objectivec
[UITools assignBackgroundParallaxBehavior:self.backgroundView];

[UITools assignForegroundParallaxBehavior:self.foregroundViews];
```
#### Create the View Controllers

No let's create 5 new ViewControllers: 

  * AboutViewController
  * SettingsScoreViewController
  * AddHighScoreViewController
  * HighScoreViewController
  * GameViewController

[![](/assets/wp-content/uploads/2014/02/ViewControllers4-1.jpg)](/assets/wp-content/uploads/2014/02/ViewControllers4-1.jpg)

I'll organize all ViewControllers in a group (File -> New -> Group) 

[![](/assets/wp-content/uploads/2014/02/ViewControllers5.png)](/assets/wp-content/uploads/2014/02/ViewControllers5.png)

#### Repeat the following steps for each View Controller:

#### 1. Add properties to header files:

```objectivec
@property (weak, nonatomic) IBOutlet UIImageView *backgroundView;
@property (strong, nonatomic) IBOutletCollection(UIView) NSArray *foregroundViews;
```

#### 2. Import helper class:

```objectivec
#import "UITools.h"
```

#### 3. Assign parallax behavior in ViewDidLoad
```objectivec
- (void)viewDidLoad {
  [super viewDidLoad];

  // Do any additional setup after loading the view.
  [UITools assignBackgroundParallaxBehavior:self.backgroundView];
  [UITools assignForegroundParallaxBehavior:self.foregroundViews];
}
```

#### 4. Open the iPhone Storyboard and add a new ViewController

[![](/assets/wp-content/uploads/2014/02/ViewControllers6-1.jpg)](/assets/wp-content/uploads/2014/02/ViewControllers6-1.jpg)

#### 5. Change orientation to landscape and statusbar to none

[![](/assets/wp-content/uploads/2014/02/ViewControllers8.png)](/assets/wp-content/uploads/2014/02/ViewControllers8.png)

#### 6. Change class to one of the just created ViewControllers

[![](/assets/wp-content/uploads/2014/02/ViewControllers7.png)](/assets/wp-content/uploads/2014/02/ViewControllers7.png)

#### 7. Add Background image, header label and buttons. Connect them with the outlets from the corresponding ViewController:

```objectivec
@property (weak, nonatomic) IBOutlet UIImageView *backgroundView;
@property (strong, nonatomic) IBOutletCollection(UIView) NSArray *foregroundViews;
```

Detailed steps are described in [part 1](/howto-design-for-depth-creating-a-start-screen-with-parallax-animations-using-ios-7-motion-effects). The result should look like this: 

[![](/assets/wp-content/uploads/2014/02/ViewControllers9-1.jpg)](/assets/wp-content/uploads/2014/02/ViewControllers9-1.jpg)

To ensure a correct sizing and alignment on the different iPhone screens (4 inch and 3.5 inch) set the autosizing options for all Buttons and Labels like this:

[![](/assets/wp-content/uploads/2014/02/ViewControllers14-1.jpg)](/assets/wp-content/uploads/2014/02/ViewControllers14-1.jpg)

[![](/assets/wp-content/uploads/2014/02/ViewControllers15-1.jpg)](/assets/wp-content/uploads/2014/02/ViewControllers15-1.jpg)

#### 8. Create Segues to navigate between the view controllers:

**8a:** Mark About button on the StartScreenViewController.

[![](/assets/wp-content/uploads/2014/02/ViewControllers10-1.jpg)](/assets/wp-content/uploads/2014/02/ViewControllers10-1.jpg)

**8b:** CTRL + Mouse click -> move mouse pointer into AboutViewController -> release 

[![](/assets/wp-content/uploads/2014/02/ViewControllers11-1.jpg)](/assets/wp-content/uploads/2014/02/ViewControllers11-1.jpg)

**8c:** Choose modal from the pop up menu 

**8d:** Repeat 8a, 8b, 8c for all transitions between our view controllers, as described in the table at the beginning of this post.

The result should look like this:

[![](/assets/wp-content/uploads/2014/02/ViewControllers12-1.jpg)](/assets/wp-content/uploads/2014/02/ViewControllers12-1.jpg)

The transition type can be changed in the menu at the right (the segue must be selected) 

[![](/assets/wp-content/uploads/2014/02/ViewControllers13.png)](/assets/wp-content/uploads/2014/02/ViewControllers13.png)


[![Video](/assets/wp-content/uploads/2014/02/Video.png)](https://www.youtube.com/watch?v=pBrYeJxmPqk)


#### Repeat step 4 till 8 for iPad.

That's all for today Cheers, 

Stefan

[Download the project from GitHub: v0.2.1](https://github.com/stfnjstn/MyFirstGame/releases/tag/v0.2.1)

---
layout: post
permalink: /howto-design-for-depth-creating-a-start-screen-with-parallax-animations-using-ios-7-motion-effects/
title: 'HowTo: Design for depth'
seo_title: Design for depth - Parallax Animation using iOS motion effects
description: game development tutorial, ios motion effects, uiview, motion effects,
  Tutorial, iOS7, Parallax, depth, howto,
date: 2014-02-10 21:54:00 -0000
last_modified_at: 2020-05-27 16:40:54 -0000
publish: true
pin: false
categories:
- iOS
- ObjectiveC
- Parallax Effect
- Storyboard
tags:
- Motion Effects
---
## Creating a start screen with parallax animations using iOS motion effects:

One highly noticed innovation in iOS 7 was the parallax effect on the home screen. When you tilt your device this gives you the impression of depth. Luckily it is incredible easy to implement this behaviour with the iOS 7 motion effects.

First you need a background which is larger than the screen and some foreground elements like Buttons, Labels, ...:

![iOS Motion Effects](/assets/2014/02/parallax1-1.jpg)

When the device is tilted, the background image must move in the opposite direction. In the example _below down_ \- the foreground elements have to move _up_. To enhance the impression of depth, it is also important that the movement of the background image is larger than the movement of the foreground elements like the buttons:

![iOS Motion Effects](/assets/2014/02/parallax2-1.jpg)

### Now let's code

First of all create a new _Single View_ Xcode project.

![iOS Motion Effects](/assets/2014/02/Parallax3-1.jpg)

Choose _Universal_ to target iPhone and iPad:

![iOS Motion Effects](/assets/2014/02/Parallax4-1.jpg)

Limit supported orientations to landscape:

![iOS Motion Effects](/assets/2014/02/Parallax5-1.jpg)

Create a new _ViewController_ and name it _StartScreenViewController_.

![iOS Motion Effects](/assets/2014/02/Parallax6-1.jpg)

![iOS Motion Effects](/assets/2014/02/Parallax7-1.jpg)

After that delete the generic ViewController which was created automatically by XCode:

![iOS Motion Effects](/assets/2014/02/Parallax8-1.jpg)

Open the iPhone Storyboard, change type of the ViewController to our new created StartScreenViewController and select landscape orientation:

![iOS Motion Effects](/assets/2014/02/Parallax9.png)

![iOS Motion Effects](/assets/2014/02/Parallax10.png)

Because we are building a game, which runs only in landscape mode, we can switch off Auto Layout.

![iOS Motion Effects](/assets/2014/02/Parallax11.png)

Now, let's create the Start Screen. Add an _UIImageView_ with a background image, a Label and 4 Buttons to the screen. I've chosen white as background color and an opacity of 0.9. After that, the screen should look like this:

![iOS Motion Effects](/assets/2014/02/Parallax12.png)

![iOS Motion Effects](/assets/2014/02/Parallax13-1.jpg)

![iOS Motion Effects](/assets/2014/02/Parallax14.png)

Now let's create the corresponding outlets to get access to the UIElements from inside of our ViewController. (Use CTRL & Drag and the Split Screen View from XCode to connect the elements).

![iOS Motion Effects](/assets/2014/02/Parallax15-1.jpg)

 

For the foreground elements choose an Outlet Collection of type UIView:

![iOS Motion Effects](/assets/2014/02/Parallax20-1.jpg)

![iOS Motion Effects](/assets/2014/02/Parallax21-1.jpg)

Now, everything is prepared to add the parallax effect. Therefore we'll create two functions which will handle the device motion and the movement of our UI elements to the StartScreenViewController class:
```objectivec
-(void)assignBackgroundParallaxBehavior:(UIView*) view {
  CGRect frameRect = view.frame;

  // increase size of screen for 20%
  frameRect.size.width = view.frame.size.width * 1.2;
  frameRect.size.height = view.frame.size.height * 1.2;
 
  // Set origin to the center of the resized frame
  frameRect.origin.x=(view.frame.size.width-frameRect.size.width)/2;
  frameRect.origin.y=(view.frame.size.height-frameRect.size.height)/2;
  view.frame = frameRect;

  // Create horizontal motion effect
  UIInterpolatingMotionEffect *horizontalMotionEffect = [[UIInterpolatingMotionEffect alloc] initWithKeyPath:@"center.x" type:UIInterpolatingMotionEffectTypeTiltAlongHorizontalAxis];

  // Limit movement of the motion effect
  horizontalMotionEffect.minimumRelativeValue = @(frameRect.origin.x);
  horizontalMotionEffect.maximumRelativeValue = @(-frameRect.origin.x);
  
  // Assign horizontal motion effect to view
  [view addMotionEffect:horizontalMotionEffect];
  
  // Create vertical motion effect
  UIInterpolatingMotionEffect *verticalMotionEffect = [[UIInterpolatingMotionEffect alloc] initWithKeyPath:@"center.y" type:UIInterpolatingMotionEffectTypeTiltAlongVerticalAxis];

  // Limit movement of the motion effect
  verticalMotionEffect.minimumRelativeValue = @(frameRect.origin.y);
  verticalMotionEffect.maximumRelativeValue = @(-frameRect.origin.y);

  // Assign vertical motion effect to view
  [view addMotionEffect:verticalMotionEffect];
}

-(void)assignForegroundParallaxBehavior:(NSArray*) view {
  int iMotionEffectSteps=20;

  // Create horizontal motion effect
  UIInterpolatingMotionEffect *horizontalMotionEffect = [[UIInterpolatingMotionEffect alloc] initWithKeyPath:@"center.x" type:UIInterpolatingMotionEffectTypeTiltAlongHorizontalAxis];
  horizontalMotionEffect.minimumRelativeValue = @(iMotionEffectSteps);
  horizontalMotionEffect.maximumRelativeValue = @(-iMotionEffectSteps);

  // Create vertical motion effect
  UIInterpolatingMotionEffect *verticalMotionEffect = [[UIInterpolatingMotionEffect alloc] initWithKeyPath:@"center.y" type:UIInterpolatingMotionEffectTypeTiltAlongVerticalAxis];
  verticalMotionEffect.minimumRelativeValue = @(iMotionEffectSteps);
  verticalMotionEffect.maximumRelativeValue = @(-iMotionEffectSteps);

  // Assign motion effects to every view of the outlet collection
  for (int i=0; i<view.count; i++) {
    [view[i] addMotionEffect:horizontalMotionEffect];
    [view[i] addMotionEffect:verticalMotionEffect];
  }
}
```

Call these methods at the end off the _viewDidLoad_ function:
```objectivec
-(void)viewDidLoad {
  [super viewDidLoad];

  // Do any additional setup after loading the view.
  [self assignBackgroundParallaxBehavior:self.backgroundView];
  [self assignForegroundParallaxBehavior:self.foregroundViews];
}
```
Test it on a device 

.... Nice!



[![Video](/assets/2014/02/Video0.png)](https://youtu.be/3FFoO4yUMx0)

Do the same for iPad

 

That's all for today.

Cheers,  
Stefan

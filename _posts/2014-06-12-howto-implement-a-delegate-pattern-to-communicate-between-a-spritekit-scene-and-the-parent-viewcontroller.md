---
layout: post
permalink: /howto-implement-a-delegate-pattern-to-communicate-between-a-spritekit-scene-and-the-parent-viewcontroller/
title: 'HowTo: Implement a Delegate Pattern to communicate between a SpriteKit Scene
  and the parent ViewController'
seo_title: 'HowTo: Implement a Delegate Pattern in ObjectiveC'
description: 'Game development tutorial: How to use a delegate pattern to communicate
  between a ViewController which contains a SpriteKit Scene in ObjectiveC'
date: 2014-06-12 21:52:00 -0000
last_modified_at: 2020-05-27 16:40:54 -0000
publish: true
pin: false
categories:
- iOS
- ObjectiveC
- SpriteKit
- Storyboard
- UIKit
tags: []
---
### Welcome to Part 10 of my blog series about game development.

Today I'll show how to use a delegate pattern to communicate with the ViewController which contains our Scene. You can download the [project from GitHub: v0.7](https://github.com/stfnjstn/MyFirstGame/releases/tag/v0.7) if you haven't completed [part 8](/howto-implement-a-hud-in-spritekit). One of the most important characteristics of this pattern is _Inversion of control_. The goal of this principle is to remove dependencies between objects. The main idea is that a _delegator_ object _delegates_ the execution a task to a _delegate object_. You can find multiple definitions and tutorials about the [Delegate Pattern](http://en.wikipedia.org/wiki/Delegation_pattern). Therefore I'll not explain the pattern itself, but show how you can use it for the following Situation:


After creating a new SpriteKit project you typically have a ViewController which has a reference to a SKScene object:

![SpriteKit project](/assets/2014/06/Bildschirmfoto-2014-06-10-um-23.10.57-1.jpg)

The ViewController presents the screen and starts the game. This works fine as long as the game lasts. But what can you do, if the game is over?

![ViewController](/assets/2014/06/Bildschirmfoto-2014-06-10-um-23.11.09-1.jpg)

Here comes the Delegate Pattern:

![Delegate Pattern](/assets/2014/06/Bildschirmfoto-2014-06-10-um-23.11.19-1.jpg)

First of all you have to specify a protocol with the methods _gameStop_ and _gameOver_ in _GameScene.h_:
```objectivec
@protocol GameSceneDelegate <NSObject>

@required

-(void) gameStop;

-(void) gameOver;

@end
```
The Scene object needs a property to store the reference of the Delegate in _GameScene.h_:
```objectivec
@property (nonatomic,strong)  id<GameSceneDelegate> delegateContainerViewController; The ViewController which will act as Delegate has to implement the protocol:

@interface GameViewController : UIViewController <GameSceneDelegate>
```

set the delegateContainerViewController property for the Scene:
```objectivec
-(void)viewWillAppear:(BOOL)animated{
  ...
  // Present the scene.
  [skView presentScene:gameScene];
  gameScene.delegateContainerViewController=self;
  }
```

GameScene and GameViewController have to call/react on the protocol methods:

![GameViewController](/assets/2014/06/Bildschirmfoto-2014-06-10-um-23.11.27-1.jpg)

Add this method to GameScene.m to notify the GameViewController with _gameStop_ and _gameOver_:

```objectivec
// React on Alert
- (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex {
  if (alertView.tag==1) {
    if (buttonIndex==1) {
      // Notify Delegate
      [self.delegateContainerViewController gameStop];
    }
  } else if (alertView.tag==2) {
    // Notify Delegate
    [self.delegateContainerViewController gameOver];
  }
}
```

The GameViewController has to react on _gameStop_ and _gameOver_. For example by navigating to another ViewController. Add this two methods to GameViewController.m:
```objectivec
-(void) gameStop {
  [self performSegueWithIdentifier: @"BackToStart" sender: self];
}

-(void) gameOver {
  [self performSegueWithIdentifier: @"AddHighScore" sender: self];
}
```

``performSegueWithIdentifier`` navigates to another ViewController as specified in the iPhone and iPad storyboards. The only missing thing is to name the segues in the storyboards with ``BackToStart`` and ``AddHighScore``:

![performSegueWithIdentifier](/assets/2014/06/Bildschirmfoto-2014-06-12-um-23.38.33-1.jpg)

As always you can download the complete [project from GitHub: v0.8](https://github.com/stfnjstn/MyFirstGame/releases/tag/v0.8) That's all for today. In my next post I'll try something with [SWIFT](https://itunes.apple.com/us/book/swift-programming-language/id881256329?mt=11).

Cheers,  
Stefan

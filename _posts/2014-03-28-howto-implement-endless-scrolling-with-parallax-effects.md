---
layout: post
permalink: /howto-implement-endless-scrolling-with-parallax-effects/
title: 'HowTo: Implement endless scrolling with parallax effects'
seo_title: 'HowTo: Implement endless scrolling with parallax effects'
description: SpriteKit, parallax effect, infinite scrolling, iOS, objectivec, game
  development, tutorial, endless scrolling
date: 2014-03-28 22:19:00 -0000
last_modified_at: 2020-05-27 16:40:55 -0000
publish: true
pin: false
categories:
- iOS
- ObjectiveC
- Parallax Effect
- Scrolling
- UIKit
tags: []
---
### Welcome to Part 5 of my blog series about game development: Endless Scrolling

Today I'll create a component which implements the endless scrolling and adds some parallax effects. I'll use SpriteKit for that. A nice tutorial about SpriteKit can be found here and [here](http://www.raywenderlich.com/42699/spritekit-tutorial-for-beginners) and [here](https://developer.apple.com/library/ios/documentation/GraphicsAnimation/Conceptual/SpriteKit_PG/Introduction/Introduction.html).

### If you haven't completed[ part 3 or 4](https://developerplayground.net/?p=27), you can [download the project from GitHub: v0.3](https://github.com/stfnjstn/MyFirstGame/releases/tag/v0.3)

First of all we need some background images to show the infinite parallax scrolling. I've created four layers:

### Background:

[![](/assets/wp-content/uploads/2014/03/Background-568h@2xiphone-1.jpg)](/assets/wp-content/uploads/2014/03/Background-568h@2xiphone-1.jpg)

#### BackgroundBush:

[![](/assets/wp-content/uploads/2014/03/BackgroundBushiPad@2x-1.jpg)](/assets/wp-content/uploads/2014/03/BackgroundBushiPad@2x-1.jpg)

#### BackgroundTree:

[![](/assets/wp-content/uploads/2014/03/BackgroundTree@2xipad-1.jpg)](/assets/wp-content/uploads/2014/03/BackgroundTree@2xipad-1.jpg)

#### BackgroundGrass:

[![](/assets/wp-content/uploads/2014/03/BackgroundGrassiPad@2x-1.jpg)](/assets/wp-content/uploads/2014/03/BackgroundGrassiPad@2x-1.jpg)

#### Combining all images together looks like this:

[![](/assets/wp-content/uploads/2014/03/BackgroundPara-1.jpg)](/assets/wp-content/uploads/2014/03/BackgroundPara-1.jpg)

### Adding the images to out XCode project:

The size of textures for SKSpriteNode is limited. Therefore I'll slice the background into tiles:

[![](/assets/wp-content/uploads/2014/03/Endless12-1.jpg)](/assets/wp-content/uploads/2014/03/Endless12-1.jpg)

For example the Background image is only shown fullscreen without scrolling. The Bush background has a size of 4 screens. It is used for scrolling. Remember my last post: The first and the last screen must be identical!

One principle from the Apple design guidelines to provide an excellent user experience is: Do not scale!

That means we need multiple versions of our images in different resolutions.

(=> 4 versions, if we limit our target platform to iOS 7 or newer.)

[![](/assets/wp-content/uploads/2014/03/Endless15-1.jpg)](/assets/wp-content/uploads/2014/03/Endless15-1.jpg)

Add the images to the Asset Catalog. If you are not familiar with Asset Catalog, Apple has a nice tutorial [here](https://developer.apple.com/library/ios/recipes/xcode_help-image_catalog-1.0/AddingImageSets/AddingImageSets.html).

[![](/assets/wp-content/uploads/2014/03/Endless2-1.jpg)](/assets/wp-content/uploads/2014/03/Endless2-1.jpg)

[![](/assets/wp-content/uploads/2014/03/Endless3.png)](/assets/wp-content/uploads/2014/03/Endless3.png)

[![](/assets/wp-content/uploads/2014/03/Bildschirmfoto-2014-04-06-um-09.36.43-1.jpg)](/assets/wp-content/uploads/2014/03/Bildschirmfoto-2014-04-06-um-09.36.43-1.jpg)

## Adding a SpriteKit Scene to our ViewController:

Now after creating many different images let's start coding ...

#### 1\. Add the SpriteKit Library to the project

Press '+' to add a new library

[![](/assets/wp-content/uploads/2014/03/Endless5.png)](/assets/wp-content/uploads/2014/03/Endless5.png)

Choose SpriteKit.framework

[![](/assets/wp-content/uploads/2014/03/Endless6-1.jpg)](/assets/wp-content/uploads/2014/03/Endless6-1.jpg)

Add an import statement for SpriteKit to the MyFirstGame-Prefix.pch file

[![](/assets/wp-content/uploads/2014/03/Endless7.png)](/assets/wp-content/uploads/2014/03/Endless7.png)

#### 2\. Create a new Scene:

Add a new file with type Objective-c class:

[![](/assets/wp-content/uploads/2014/03/Endless8-1.jpg)](/assets/wp-content/uploads/2014/03/Endless8-1.jpg)

New file must be a subclass of SKScene:

A [SKScene](https://developer.apple.com/library/ios/documentation/SpriteKit/Reference/SKScene_Ref/Reference/Reference.html) represents the content of a scene in Sprite Kit. It is the root node of other Sprite Kit nodes (SKNode)

[![](/assets/wp-content/uploads/2014/03/Endless9-1.jpg)](/assets/wp-content/uploads/2014/03/Endless9-1.jpg)

Add another file to implement the endless scrolling:

This file must be a subtype of [SKNode](https://developer.apple.com/library/ios/documentation/SpriteKit/Reference/SKNode_Ref/Reference/Reference.html). A SKNode object can be added to our scene. It's also possible to other nodes in a hierarchical order, one for every background.

[![](/assets/wp-content/uploads/2014/03/Endless10-1.jpg)](/assets/wp-content/uploads/2014/03/Endless10-1.jpg)

#### 3\. Implement ParallaxHandlerNode

This class is derived from SKNode. It is the root element for all backgrounds/tiles which are created for the endless scrolling:

ParallaxHandlerNode.h:

#import <SpriteKit/SpriteKit.h>

@interface ParallaxHandlerNode : SKNode

-(id)initWithSize:(CGSize)Size;

-(void)addBackgroundLayer:(NSArray*)tiles;

-(void)scroll:(float)speed;

@end

The ParallaxHandlerNode class implements three methods:

  * initWithSize \- initializes the object
  * addBackgroundLayer \- adds a layer to the parallax hierarchy
  * scroll \- implements the endless scrolling for all layers



ParallaxHandlerNode.m:
```
#import "ParallaxHandlerNode.h"

@implementation ParallaxHandlerNode

CGSize _containerSize;

-(id)initWithSize:(CGSize)size {

_containerSize=size;

return [self init];

}

// Add a background layer.

-(void)addBackgroundLayer:(NSArray*)tiles {

// Create static background

if ([tiles count]==1 ) {

SKSpriteNode *background=[SKSpriteNode spriteNodeWithImageNamed:(NSString*)[tiles objectAtIndex:0]];

background.position=CGPointMake(_containerSize.width/2, _containerSize.height/2);

[self addChild:background];

} else {

// Create a background for infinite scrolling

// Create a SKNode a root element

SKNode *background=[[SKNode alloc]init];

[self addChild:background];

// Create and add tiles to the node

for (int i=0; i<[tiles count]; i++) {

NSString *item = [tiles objectAtIndex:i];

SKSpriteNode *tile;

if (![item isEqualToString: @""]) {

// Add an emtpy screen

tile=[SKSpriteNode spriteNodeWithImageNamed:item];

tile.position=CGPointMake(_containerSize.width/2+(i*_containerSize.width), 0);

} else {

tile=[[SKSpriteNode alloc] init];

tile.size=_containerSize;

tile.position=CGPointMake(_containerSize.width/2+(i*_containerSize.width), _containerSize.height/2);

}

[background addChild:tile];

}

// position background at the second screen

background.position=CGPointMake(-_containerSize.width, _containerSize.height/2);

}

}

// Infinite scrolling:

// - Scroll the backgrounds and switch back if the end or the start screen is reached

// - Speed depends on layer to simulare deepth

-(void)scroll:(float)speed {

for (int i=0; i<self.children.count;i++) {

SKNode *node = [self.children objectAtIndex:i];

// If more than one screen => Scrolling

if (node.children.count>0) {

float parallaxPos=node.position.x;

NSLog(@"x: %f", parallaxPos);

if (speed>0) {

parallaxPos+=speed*i;

if (parallaxPos>=0) {

// switch between first and last screen

parallaxPos=-_containerSize.width*(node.children.count-1);

}

} else if (speed<0) {

parallaxPos+=speed*i;

if (parallaxPos<-_containerSize.width*(node.children.count-1)) {

// switch between last and first screen

parallaxPos=0;

}

}

// Set new node position. Position can't be set directly, therefore tempPos is used.

CGPoint tmpPos=node.position;

tmpPos.x = parallaxPos;

node.position = tmpPos;

}

}

}

@end
```

#### 4\. Create the scene:

The GameScene class is inherited from SKScene and implements four methods:

  * initWithSize \- initializes the object
  * touchesBegan \- reacts on touch events, changes speed and direction
  * addBackgrounds \- adds the background layers
  * update \- the game loop



GameScene.m:
```
#import "GameScene.h"

#import "ParallaxHandlerNode.h"

// Constants

#define cStartSpeed 5

#define cMaxSpeed 80

@implementation GameScene

// private properties

NSTimeInterval _lastUpdateTime;

NSTimeInterval _dt;

int _speed=cStartSpeed;

ParallaxHandlerNode *background;

-(id)initWithSize:(CGSize)size {

if (self = [super initWithSize:size]) {

[self addBackgrounds];

}

return self;

}

// Increase speed after touch event up to 5 times.

// After maximum speed is reached the next touch changes the scroll direction

-(void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event {

if (_speed<cMaxSpeed && _speed>-cMaxSpeed) {

_speed=_speed*2;

} else {

if (_speed<0) {

_speed=cStartSpeed;

} else {

_speed=-cStartSpeed;

}

}

}

// Add the background elements for parallax scrolling

-(void)addBackgrounds {

// Array contains the name of the background tiles. "" for adding an empty screen

NSArray *nameBackground = [NSArray arrayWithObjects: @"Background", nil];

NSArray *nameBush = [NSArray arrayWithObjects:@"BackgroundBushLeft", @"BackgroundBushRight", @"", @"BackgroundBushLeft", nil];

NSArray *nameTree = [NSArray arrayWithObjects:@"BackgroundTreeLeft", @"BackgroundTreeRight", @"BackgroundTreeLeft" ,nil];

NSArray *nameGrass = [NSArray arrayWithObjects:@"", @"BackgroundGrassCenter", @"", nil];

// Root node which contains the tree of backgrounds/background tiles

background = [[ParallaxHandlerNode alloc] initWithSize:self.size];

[self addChild:background];

[background addBackgroundLayer:nameBackground];

[background addBackgroundLayer:nameBush];

[background addBackgroundLayer:nameTree];

[background addBackgroundLayer:nameGrass];

}

// The GameLoop

-(void)update:(NSTimeInterval)currentTime {

// Needed for smooth scrolling. It's not guaranteed, that the update method is not called in fixed intervalls

if (_lastUpdateTime) {

_dt = currentTime - _lastUpdateTime;

} else {

_dt = 0;

}

_lastUpdateTime = currentTime;

// Scroll

[background scroll:_speed*_dt];

}

@end

#### 5\. Add the scene to GameViewController:

Add this method to GameViewController.h

-(void)viewWillAppear:(BOOL)animated{

[super viewWillAppear:animated];

SKView * skView = [[SKView alloc]initWithFrame:self.view.frame]; //(SKView *)self.view;

[self.view addSubview:skView];

skView.showsFPS = YES;

skView.showsNodeCount = YES;

// Create and configure the scene.

GameScene *gameScene = [GameScene sceneWithSize:skView.bounds.size];

gameScene.scaleMode = SKSceneScaleModeResizeFill; //SKSceneScaleModeAspectFill;

// Present the scene.

[skView presentScene:gameScene];

}
```
#### 6\. Deploy and run

That's all for today.

Cheers,   
Stefan

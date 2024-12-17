---
layout: post
permalink: /howto-extend-endless-horizontal-scrolling-with-a-vertical-parallax-effect/
title: 'HowTo: Extend endless horizontal scrolling with a vertical parallax effects'
seo_title: 'HowTo: Implement Scrolling with parallax effects in iOS'
description: Scrolling with parallax effects, endless scrolling, game development,
  iOS, objectivec, tutorial
date: 2014-05-05 21:47:00 -0000
last_modified_at: 2020-05-27 16:40:54 -0000
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
### Welcome to Part 7 of my blog series about game development: Scrolling with parallax effects

Today I'll extend the parallax effect from [part 5](/howto-implement-endless-scrolling-with-parallax-effects) of my posts with vertical scrolling. This should increase the illusion of depth. To control the movement I'll use the motion sensors as described in [part 6.](/howto-use-the-device-motion-sensors-to-control-your-game)

### Steps to achieve this behavior:

  * Scale the width and the height of the background image and implement horizontal and vertical movement of the background image:

[![](/assets/wp-content/uploads/2014/05/Parallax-2-1-1.jpg)](/assets/wp-content/uploads/2014/05/Parallax-2-1-1.jpg)

  * Scale the height of the background tiles which are used for endless scrolling and implement vertical movement for the background tiles:

[![](/assets/wp-content/uploads/2014/05/Parallax-2-2-1.jpg)](/assets/wp-content/uploads/2014/05/Parallax-2-2-1.jpg)

  * Some tricks to get a better effect:
    * Use different scale factors for the backgrounds. Farer away means bigger scale factor
    * Move backgrounds with different speed. The background which is farest away should be the fastest.
    * Move the background image in another direction as the tile backgrounds images
    * Physically this is not correct, but enough to create a good illusion. Otherwise the player is distracted to much by the movements



### Here's a video which shows the effect:

[![Video](/assets/wp-content/uploads/2014/05/Video0.png)](https://youtu.be/y5llMUVmZhU)


**Now let's integrate this into the MyFirstGame project:**

The code changes should be straight forward: (If you haven't completed [part 6](/howto-use-the-device-motion-sensors-to-control-your-game) you can download the project from GitHub: [v0.5.1](https://github.com/stfnjstn/MyFirstGame/releases/tag/v0.6))

#### Changes in "ParallaxHandlerNode.h":
s
-(void)addBackgroundLayer:(NSArray*)tiles DirectionY:(int)directionY StepSize:(float)stepSize ScaleFactorX:(float)scaleFactorX ScaleFactorY:(float)scaleFactorY;
```
#### Complete "ParallaxHandlerNode.m":

The main changes are done in:

  * ``addBackgroundLayer``: Extend the method signature to get the scaling and movement informations. Scale the images.
  * ``scroll``: Implement the additional parallax effects


```objectivec
#import "ParallaxHandlerNode.h"
#define cFactorForAngleToGetSpeedX 6
#define cFactorForAngleToGetSpeedY 1.5

@implementation ParallaxHandlerNode
  CGSize _containerSize;
  NSMutableArray* _directions;
  NSMutableArray* _stepsizes;

  -(id)initWithSize:(CGSize)size {
    _containerSize=size;
    
    // Initialize the Arrays to store the direction and stepsize information
    _directions = [[NSMutableArray alloc] init];
    _stepsizes = [[NSMutableArray alloc] init];
    return [self init];
  }

  // Add a background layer.
  -(void)addBackgroundLayer:(NSArray*)tiles DirectionY:(int)directionY StepSize:(float)stepSize ScaleFactorX:(float)scaleFactorX ScaleFactorY:(float)scaleFactorY{
    [_directions addObject:[NSNumber numberWithInt:directionY]];
    [_stepsizes addObject:[NSNumber numberWithFloat:stepSize]];

    // Create static background
    if ([tiles count]==1 ) {
      SKSpriteNode *background=[SKSpriteNode spriteNodeWithImageNamed:(NSString*)[tiles objectAtIndex:0]];
      // Scale size to enable parallax effect
      background.size=CGSizeMake(background.size.width*scaleFactorX, background.size.height*scaleFactorY);
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
          // Scale size to enable parallax effect
          tile.size=CGSizeMake(tile.size.width, tile.size.height * scaleFactorY);
          tile.position=CGPointMake(_containerSize.width/2+(i*_containerSize.width), (_containerSize.width-tile.size.width)/2);
        } else {
          tile=[[SKSpriteNode alloc] init];
          // Scale size to enable parallax effect
          tile.size=CGSizeMake(_containerSize.width, _containerSize.height * scaleFactorY);
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
  // - Speed depends on layer to simulate deepth
  -(void)scroll:(float)speed {
    GLKVector3 vMotionVector = [MotionManagerSingleton getMotionVectorWithLowPass];
    float dMotionFactorX=vMotionVector.x*cFactorForAngleToGetSpeedX;
    float dMotionFactorY=vMotionVector.y*cFactorForAngleToGetSpeedY;
    CGPoint parallaxPos;
    for (int i=0; i<self.children.count;i++) {
      SKNode *node = [self.children objectAtIndex:i];
      SKSpriteNode *spriteNode;
      parallaxPos=node.position;
      
      // If more than one screen => Scrolling with tiles
      if (node.children.count>0) {
        spriteNode = (SKSpriteNode*)[node.children objectAtIndex:0];
        parallaxPos.x+=speed*(i+1)*dMotionFactorX; //Changed
        if (dMotionFactorX>0) {
          if (parallaxPos.x>=0) {
            // switch between first and last screen
            parallaxPos.x=-_containerSize.width*(node.children.count-1);
          }
        } else if (dMotionFactorX<0) {
          if (parallaxPos.x<-_containerSize.width*(node.children.count-1)) {
            // switch between last and first screen
            parallaxPos.x=0;
          }
        }
      } else {
        spriteNode = (SKSpriteNode*)node;
        float dDiff=(spriteNode.size.width \- _containerSize.width)/2;
        parallaxPos.x+=speed*(i+1)*dMotionFactorX;
        if (dMotionFactorX>0) {
          if (parallaxPos.x>=_containerSize.width/2+dDiff) {
            parallaxPos.x=_containerSize.width/2+dDiff;
          }
        } else if (dMotionFactorX<0) {
          if (parallaxPos.x<_containerSize.width/2-dDiff) {
            parallaxPos.x=_containerSize.width/2-dDiff;
          }
        }
      }

      // Vertical scrolling
      float dDiffY=(spriteNode.size.height \- _containerSize.height)/2; // pixels above and below to scroll
      float dStepSize=[[_stepsizes objectAtIndex:i] floatValue]; // Scrolling speed depends on level
      int iDirection=[[_directions objectAtIndex:i] intValue]; // Scroll backgroundimage in another direction to enhance parallax effect
      parallaxPos.y+=speed*dStepSize*dMotionFactorY*iDirection; // Calculate new position

      // Check if bounds are reached
      if (dMotionFactorY*iDirection>0) {
        if (parallaxPos.y>=_containerSize.height/2+dDiffY) {
          parallaxPos.y=_containerSize.height/2+dDiffY;
        }
      } else {
        if (parallaxPos.y<_containerSize.height/2-dDiffY) {
          parallaxPos.y=_containerSize.height/2-dDiffY;
        }
      }

      // Set the new position
      node.position = parallaxPos;
    }
  }
@end
```

#### Changes in "GameScene.m":
```objectivec
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

  // Move background which is farest away fastest => Physically not correct, but enough to realize illusion of depths. Otherwise the player is distracted to much by the movements
  [background addBackgroundLayer:nameBackground DirectionY:-1 StepSize:0.9 ScaleFactorX:1.2 ScaleFactorY:1.09];
  [background addBackgroundLayer:nameBush DirectionY:1 StepSize:0.7 ScaleFactorX:1.0 ScaleFactorY:1.07];
  [background addBackgroundLayer:nameTree DirectionY:1 StepSize:0.5 ScaleFactorX:1.0 ScaleFactorY:1.05];
  [background addBackgroundLayer:nameGrass DirectionY:1 StepSize:0.3 ScaleFactorX:1.0 ScaleFactorY:1.03];
}
```

You can play around with the values to find the optimal solution for your needs

As always you can download the complete [project from GitHub: v0.6.1](https://github.com/stfnjstn/MyFirstGame/releases/tag/v0.6.1)

That's all for today. In my next post I'll use a Delegate Pattern to add a HUD (Head Up Display) to my game.

Cheers,   
Stefan
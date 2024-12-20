---
layout: post
permalink: /howto-add-splash-screen-application-icons/
title: 'HowTo: Add Splash Screen & Application Icons'
seo_title: Add iOS Splash Screen & Application Icons
description: game development tutorial, iOS, splashscreen, asset catalog, app icon,
  xcode, objectivec, hide Statusbar
date: 2014-03-04 22:47:00 -0000
last_modified_at: 2020-05-27 16:40:54 -0000
publish: true
pin: false
categories:
- iOS
- Xcode
tags: []
---
### Welcome to Part 3 of my blog series about game development.

Today I'm adding the app icons and a splash screen. I'll use an [asset catalog](https://developer.apple.com/library/ios/recipes/xcode_help-image_catalog-1.0/Recipe.html#//apple_ref/doc/uid/TP40013303-CH1-SW1) for that. If you haven't completed [part 2](/howto-add-view-controllers-to-the-game-storyboard-and-use-segues-to-navigate-between-them) , you can [download the project from GitHub: v0.2.1](https://github.com/stfnjstn/MyFirstGame/releases/tag/v0.2.1)

### First of all let's hide the annoying header bar:

[![](/developerplayground/assets/2014/03/Splash1-1.jpg)](/developerplayground/assets/2014/03/Splash1-1.jpg)

You have to add to entries in the ``plist`` file: ``Supporting Files/MyFirstGame-Info.plist``

[![](/developerplayground/assets/2014/03/Splash2.png)](/developerplayground/assets/2014/03/Splash2.png)

  * ``Status bar is initially hidden = Yes``: Hides the status bar at application start and in the splash screen
  * ``View controller-based status bar appearance = No``: Prevents that the view controller classes show the status bar


### Create AppIcons and SplashScreen Icons with an AssetCatalog

Why an [Asset Catalog](https://developer.apple.com/library/ios/recipes/xcode_help-image_catalog-1.0/Recipe.html)? That's easy: If you compile you App for iOS 7, the images are stored in a binary. The advantage of this approach is a faster application start and also a smaller IPA file size which speeds up the download of your App. It is also much easier to manage your images. You must no longer follow strange naming conventions like ``image@2.png`` for retina and ``image.png`` for non retina devices or even more confusing ``Default-568h@2x.png`` for iPhone 5 and ``Default@2x.png`` for iPhone 4(s) splash screen.

If we limit our App to iOS 7 capable devices we need 15 different images sizes. 9 for the App Icon and 6 for SplashScreens. That sounds much, but comparing to Android devices with much more different screen resolutions, this is incredible easy.

[![](/developerplayground/assets/2014/03/Splash3.png)](/developerplayground/assets/2014/03/Splash3.png)

[![](/developerplayground/assets/2014/03/Splash4.png)](/developerplayground/assets/2014/03/Splash4.png)

Create the images and open the Asset Catalog:

[![](/developerplayground/assets/2014/03/Splash5.png)](/developerplayground/assets/2014/03/Splash5.png)

Drag the images into the Asset Catalog:

[![](/developerplayground/assets/2014/03/Splash6-1.jpg)](/developerplayground/assets/2014/03/Splash6-1.jpg)

Unfortunately the current version of XCode contains a Bug. The splash screen stays black, if we support only the landscape screen orientation on iOS 7 phones: ([iPhone landscape-only no launch image for iOS7 R4 image asset](http://stackoverflow.com/questions/19110583/iphone-landscape-only-no-launch-image-for-ios7-r4-image-asset/22106849#22106849)):

[![](/developerplayground/assets/2014/03/Splash7.png)](/developerplayground/assets/2014/03/Splash7.png)

You can either wait until Apple fixes this issue or solve it using this workaround:

Go to the project settings and select "Don't use Asset Catalog" in the launch images section. Now we can add the launch images the traditional way. I'll still use the asset catalog for the app icons and other images.

[![](/developerplayground/assets/2014/03/Splash8.png)](/developerplayground/assets/2014/03/Splash8.png)

That's all for today

Cheers, Stefan [Download the project from GitHub: v0.3](https://github.com/stfnjstn/MyFirstGame/releases/tag/v0.3)

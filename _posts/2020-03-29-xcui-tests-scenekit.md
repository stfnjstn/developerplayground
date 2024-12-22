---
layout: post
permalink: /xcui-tests-scenekit/
title: XCUI Tests with SceneKit
description: Tutorial about automated XCUI tests with SceneKit using Apples XCUI test
  framework. It shows how to find SceneKit nodes, which does not work out of the box.
date: 2020-03-29 22:14:26 -0000
last_modified_at: 2020-05-27 16:40:57 -0000
publish: true
pin: false
image:
  path: /assets/2020/03/ETMIPAD.jpg
categories:
- Test Automation
- Uncategorized
tags:
- SceneKit
- Swift
- Test Automation
- XCUI
---
I started writing UI tests for my upcoming dungeon crawler game. My game engine uses _SceneKit_ for the 3D world and _XCUI_  tests for the UI test automation.

I recommend this [tutorial](https://www.hackingwithswift.com/articles/83/how-to-test-your-user-interface-using-xcode) as introduction in ui test automation with XCUI.

I write this tutorial because there is not much information avilable about the combination of SCNKit and XCUI. Hopefully it helps to avoid some of the pitfalls.

The specific problem I had to solve, was to automate a scenario, where two or more interactive _SCNNodes_  are visible on a screen. Every node should trigger a different action.

Using screen coordinates to trigger a specific node, would have been one option, but this causes a huge overhead. My game runs on iPads and iPhones in Landscape and Portrait format. That means for each combination of screen resolution and orientation I would need different sets of coordinates.

![XCUI Test Automation with SceneKit](/assets/2020/03/PhoneUITestLandscape.jpg)

![XCUI Test Automation with SceneKit: Identify a SKNode](/assets/2020/03/iPad.jpg)

Here is a much better solution:

I subclassed _SCNNode_ and implemented the _UIAccessibilityIdentification_ delegate. Every time I created an instance of _MyNode_  I gave it a unique _accessibilityIdentifier_.

```swift  
class MyNode: SCNNode, UIAccessibilityIdentification {
    var accessibilityIdentifier: String?
}
```

Now these nodes can be addressed inside of the test code with:

```swift  
app.otherElements[id].firstMatch
```

My first try was to get the element and call the _tap_ method directly on the node:

```swift  
app.otherElements[id].firstMatch.tap()
```

Unfortunately that didn't work. An _SCNNode_ doesn't react on the _tap_ method in XCUI.

The trick was to find the _SCNNode_ , get the coordinates of the node and call _tap_ on these coordinates:

```swift 
app.otherElements[id].firstMatch.coordinate(withNormalizedOffset: CGVector.zero).tap()
```

And here is a  video with the automated result. The left button closes the pit and the right opens the door.

[![Video](/assets/Videos/YtzKKdSh1r0.png)](https://youtu.be/YtzKKdSh1r0)

That all for today,

Cheers Stefan

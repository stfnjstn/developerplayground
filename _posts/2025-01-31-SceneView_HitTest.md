---
layout: post
permalink: /SceneView_HitTest/
title: HitTests in SceneView 
date: 2025-01-31
publish: true
categories: [SceneKit, AppleWatch]
tags: []
---

## Deprecation of Storyboards for Apple Watch and usefull SceneKit Workarounds

With watchOS 10, Apple has deprecated storyboards for Apple Watch apps, requiring developers to transition fully to SwiftUI. This change forces a significant refactoring of my game !!!LINK!!! on this platform, as I relied on storyboard-based UI elements. Additionally, integrating SceneKit in SwiftUI introduces further challenges, as `SCNView` is not available on watchOS and `WKInterfaceSCNScene`, which I've used till now, is deprecated. Apple recommends to use `SceneView`. However, `SceneView` does not conform to SCNSceneRenderer, meaning essential features like `renderer(_:updateAtTime:)` as game loop and `hitTest(_:options:)` to detect elements in the scene, which are selected (hit) by tap gestures are unavailable.

In this blog post, I present a solution that overcomes these limitations.

![SceneView](/assets/2025/01/SveneView.png)


### The Solution
To resolve this, we need to:
1. Create a `GameController` class implementing `SCNSceneRendererDelegate`
2. During creation of the `SceneView` in the SwiftUI View provide this class as delegate
3. The Delegate method `(_ renderer: SCNSceneRenderer, updateAtTime time: TimeInterval)` in GameConroleer is called when the `SceneView` renders the scene.
4. Capture the `SCNSceneRenderer` instance inside `renderer` and store in a local variable `sceneRenderer`.
5. Now you can call `hitTest(_:options:)` as part of `sceneRenderer`

Big Thank You to this [stackoverflow question](https://stackoverflow.com/questions/62392363/swiftui-hittest-on-scenekit) which puts me in the right direction.

### Here’s a sample SwiftUI implementation:


```
import SwiftUI
import SceneKit

struct ContentView: View {
    var gameController = GameController()

    @State private var crownRotation: Double = 0  // Tracks Digital Crown input
    @FocusState private var isFocused: Bool  // Needed for Digital Crown input

    var body: some View {
        SceneView(
            scene: gameController.scene,
            pointOfView: gameController.cameraNode,
            options: [.allowsCameraControl],
            delegate: gameController
        )
        .focusable()
        .focused($isFocused)
        .digitalCrownRotation($crownRotation, from: -360, through: 360, by: 1, sensitivity: .low)
        .onChange(of: crownRotation) { oldValue, newValue in
            gameController.rotateShip(by: newValue)
        }
        .onAppear {
            isFocused = true  // Focus Digital Crown
        }
        .gesture(
            SpatialTapGesture(count: 1)
                .onEnded { event in
                    gameController.checkShipIsHit(at: event.location)
                }
        )
    }
}

class GameController: NSObject, SCNSceneRendererDelegate {
    let scene = SCNScene(named: "art.scnassets/ship.scn")!
    var sceneRenderer: SCNSceneRenderer?
    
    var cameraNode: SCNNode? {
        scene.rootNode.childNode(withName: "camera", recursively: false)
    }
    
    var shipNode: SCNNode? {
        scene.rootNode.childNode(withName: "shipMesh", recursively: true)
    }

    // Store renderer for hit testing
    func renderer(_ renderer: SCNSceneRenderer, updateAtTime time: TimeInterval) {
        if sceneRenderer == nil {
            sceneRenderer = renderer
        }
        // This can be used as game loop to implement game logic
    }

    // Rotate the ship based on Digital Crown input
    func rotateShip(by rotationFactor: Double) {
        shipNode?.eulerAngles.y = Float(rotationFactor / 5.0)
    }
    
    // Perform hit test to check if the ship was tapped
    func checkShipIsHit(at location: CGPoint) {
        guard let renderer = sceneRenderer else { return }
        let hits = renderer.hitTest(location, options: nil)
        
        if let tappedNode = hits.first?.node, tappedNode == shipNode {
            tappedNode.runAction(SCNAction.sequence([
                SCNAction.scale(to: 0.1, duration: 0.1),  // Quick scale up
                SCNAction.scale(to: 0.2, duration: 0.1)   // Back to normal
            ]))
        }
    }
} 
```


You will see the result in the next update of my [Dungeon Master clone:](https://apps.apple.com/app/id1502853397) 

![ETM0](/assets/2025/01/ETM0.png)| ![ETM1](/assets/2025/01/ETM1.png) | ![ETM2](/assets/2025/01/ETM2.png)
![ETM3](/assets/2025/01/ETM3.png)| ![ETM4](/assets/2025/01/ETM4.png) | ![ETM5](/assets/2025/01/ETM5.png)

That all for today,

Cheers Stefan
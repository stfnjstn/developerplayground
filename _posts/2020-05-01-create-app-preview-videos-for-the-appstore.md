---
layout: post
permalink: /create-app-preview-videos-for-the-appstore/
title: Create App Preview Videos for the Apple Appstore
description: Workflow for creating App Preview Videos for the Apple Appstore with
  iMovie. I'll also show how to scale videos for several formafactors and device.
date: 2020-05-01 13:33:43 -0000
last_modified_at: 2020-05-27 16:40:53 -0000
publish: true
pin: false
image:
  path: /assets/2020/05/AppstoreConnect.jpg
categories:
- My Games
- Test Automation
- Uncategorized
tags:
- Apple
- Appstore Connect
- Escape the Dungeon Maze
- Escape The Maze
- RPG
- Swift
- XCUI
---
I've just created a few Apple Appstore preview videos for my upcoming Dungeon Crawler game: _Escape the Dungeon Maze_.

I'll share my workflow for creating these videos in this post:

#### 1. Create an XCUI Automation Test:

The test should cover all areas which should be part of the video. It can run longer than the allowed 30 seconds. We will cut it in a later step. More about XCUI tests [here](/xcui-tests-scenekit).

![UITestSample](/assets/2020/05/UITestSample.png)

By the way: I'm using the same automated test for creating and uploading screenshots to the Appstore with [fastlane](https://fastlane.tools). Maybe I'll write a post about this in the future.

#### 2. Run the test and capture the video

I recommend adding screen recording to your control center:

![iOS Screen Recording](/assets/2020/05/ScreenRecord.jpg)

Start the screen recording on the device and then start your automated XCUI test. The test runs and everything is recorded. Once the test is completed, stop the screen recording.

#### 3. Send the video to your Mac

Use Mail, Airdrop, Files or something else for this:

![](/assets/2020/05/ShareRecordedVideo.jpg)

#### 4. Open iMovie and create a new App Preview:

![Create an App Preview in iMovie](/assets/2020/05/CreateAppPreview.jpg)

#### 5. Choose the right resolution:

Usually the typical indy developer doesn't own enough iOS devices to record an App Preview Video on every potential device type.

The trick is that iMovie App Preview takes the resolution of the first added media element for the output video. I add a black image with the needed resolution and show it only a fraction of a second at the beginning of the video.

Required resolution per device from Apple:

![App Preview Video Resolution](/assets/2020/05/AppPreviewResolutions.jpg)From Apple: <https://help.apple.com/app-store-connect/#/dev4e413fcb8>

#### 6. Add the video material

Now add the video material. iMovie will automatically scale the video during export depending on the black image at the beginning:

![Scale App Preview Video with iMovie](/assets/2020/05/BlackImageToScale.jpg)

#### 7. Export the video

![Export App Preview in iMovie](/assets/Download.svg) ![Export App Preview in iMovie](/assets/2020/05/ExportAppStore2.jpg)

#### 8. Upload the video to [Appstore Connect](https://appstoreconnect.apple.com):

![Appstore Connect Preview Video](/assets/2020/05/AppstoreConnect.jpg)

That's all for today.

Cheers  
Stefan

---
layout: post
permalink: /howto-organize-your-objective-code-with-the-pragma-mark-directive/
title: 'HowTo: Organize ObjectiveC code with the pragma mark directive'
seo_title: Organize ObjectiveC code with the pragma mark directive
description: 'I''ll only show how the ''#pragma mark'' directive can help you to organize
  your code. Keywords: iOS Game Development Blog, pragma mark directive, ObjectiveC'
date: 2014-05-28 21:32:00 -0000
last_modified_at: 2020-05-27 16:40:55 -0000
publish: true
pin: false
categories:
- iOS
- ObjectiveC
- Xcode
tags: []
---
### Welcome to Part 9 of my blog series about game development: pragma mark directive

Todays post is very short. I'll only show how the ``#pragma mark`` directive can help you to organize your code. The navigation bar on top of the code window provides the possibility to navigate in your code. Just click on the last entry:

[![](/assets/wp-content/uploads/2014/05/Bildschirmfoto-2014-05-28-um-22.55.06-1.jpg)](/assets/wp-content/uploads/2014/05/Bildschirmfoto-2014-05-28-um-22.55.06-1.jpg)

This will open a drop down list of all available constants, properties and methods. By selecting one element in the list, the code windows scrolls to the corresponding code section. So far so good, but the methods are listed in alphabetical order. This becomes quite messy if the code for your class is growing.

[![](/assets/wp-content/uploads/2014/05/Bildschirmfoto-2014-05-28-um-22.55.18-1.jpg)](/assets/wp-content/uploads/2014/05/Bildschirmfoto-2014-05-28-um-22.55.18-1.jpg)

A better way to organize your code would be grouping elements by their context. For example all methods which belongs to the HUD should be grouped together. Luckily Objective C provides a solution for that: The ``#pragma mark`` directive.

Just enter some #pragma marks to your code:
```objectivec
...

#pragma mark - Init

....

#pragma mark - HUD handling
```

You can see the result, if your click again in the navigation bar to open the drop down list:

[![](/assets/wp-content/uploads/2014/05/Bildschirmfoto-2014-05-28-um-23.07.22.png)](/assets/wp-content/uploads/2014/05/Bildschirmfoto-2014-05-28-um-23.07.22.png)

That's all for today. In my next post I'll show how to use the delegate pattern to communicate from an SKScene with the parent view controller class.

Cheers,  
Stefan

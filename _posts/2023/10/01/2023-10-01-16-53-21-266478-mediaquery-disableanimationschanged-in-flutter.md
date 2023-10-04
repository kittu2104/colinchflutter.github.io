---
layout: post
title: "MediaQuery disableAnimationsChanged in Flutter"
description: " "
date: 2023-10-01
tags: [MediaQuery]
comments: true
share: true
---

In Flutter, the `MediaQuery` class provides information about the current device's media attributes, such as its size, orientation, and more. One useful attribute provided by `MediaQuery` is the `disableAnimations` property, which indicates whether the system-wide animations are enabled or disabled.

### Introduction to disableAnimationsChanged

The `disableAnimationsChanged` event is triggered in the `MediaQuery` class whenever the system-wide animations setting changes. This can be useful for app developers who want to adjust their app's behavior based on whether animations are enabled or disabled on the device.

### Using disableAnimationsChanged

To listen for changes in the `disableAnimations` property, you need to use the `addPostFrameCallback` method of the `WidgetsBinding` class. Here's an example of how you can implement it:

```dart
import 'dart:async';
import 'package:flutter/material.dart';

class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  StreamSubscription<void> _animationSubscription;

  @override
  void initState() {
    super.initState();
    
    _animationSubscription = WidgetsBinding.instance.addPostFrameCallback((_) {
      final mediaQuery = MediaQuery.of(context);
      final disableAnimations = mediaQuery.disableAnimations;
      
      // Perform actions based on disableAnimations value
      if (disableAnimations) {
        // Animations are disabled
        // Do something here
      } else {
        // Animations are enabled
        // Do something else here
      }
    });
  }

  @override
  void dispose() {
    _animationSubscription.cancel();
    super.dispose();
  }
  
  @override
  Widget build(BuildContext context) {
    return Container(
      // Your widget code here
    );
  }
}
```

In the above example, we create a `StreamSubscription` to handle the changes in the animations setting. We use the `addPostFrameCallback` method to ensure that the callbacks are triggered after the frame has been rendered.

Inside the callback, we retrieve the `disableAnimations` property from the `MediaQuery` and perform actions based on its value.

Remember to cancel the subscription in the `dispose` method to avoid memory leaks.

### Conclusion

The `disableAnimationsChanged` event in the `MediaQuery` class allows Flutter developers to respond to changes in the system-wide animations setting. By listening to this event, you can adjust your app's behavior or UI based on whether animations are enabled or disabled on the user's device.

#Flutter #MediaQuery
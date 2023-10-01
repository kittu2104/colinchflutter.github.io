---
layout: post
title: "How to access system gesture insets using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [flutter, MediaQuery]
comments: true
share: true
---

In recent versions of Flutter, the system gesture insets have been made available to allow developers to handle screen gestures properly. System gesture insets represent the areas of the screen that are allocated for system gestures, such as swipe-up gestures to navigate back or access the home screen. By accessing these insets, you can ensure that the UI elements in your Flutter app are not obscured by the system gestures.

To access the system gesture insets, you can use the `MediaQuery` class provided by Flutter. The `MediaQuery.of(context)` method allows you to obtain the current `MediaQueryData` object, which contains various information about the device, including the system gesture insets.

Here's an example of how you can access the system gesture insets using `MediaQuery` in Flutter:

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final mediaQuery = MediaQuery.of(context);
    final systemGestureInsets = mediaQuery.viewInsets.bottom;

    // Use the systemGestureInsets to handle UI elements positioning

    return Container(
      // ...
    );
  }
}
```

In the above example, `MediaQuery.of(context)` returns the current `MediaQueryData` object. From this object, we access the `viewInsets` property, which contains information about the window margin surrounding the application interface, including the system gesture insets. Since we are interested in the bottom inset, we use `viewInsets.bottom` to access the value.

You can use the obtained `systemGestureInsets` to handle the positioning of UI elements that may be affected by system gestures. For example, if you have a bottom navigation bar, you can adjust its position to account for the system gesture insets.

Finally, remember to handle different devices and screen orientations appropriately, as the system gesture insets may vary depending on these factors.

By accessing system gesture insets using `MediaQuery` in Flutter, you can ensure that your app's UI elements are properly positioned and visible, even when system gestures are activated.

#flutter #MediaQuery
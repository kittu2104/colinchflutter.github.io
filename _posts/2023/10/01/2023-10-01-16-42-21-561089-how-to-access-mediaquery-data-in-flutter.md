---
layout: post
title: "How to access MediaQuery data in Flutter?"
description: " "
date: 2023-10-01
tags: [mediaquery]
comments: true
share: true
---

When building user interfaces in Flutter, it's important to adapt to different screen sizes and orientations. Flutter provides a `MediaQuery` class that allows us to access information about the current device's screen. With this information, we can make responsive UIs and customize our app's layout based on the available screen space.

Here's how you can access `MediaQuery` data in Flutter:

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Access the MediaQuery data using MediaQuery.of(context)
    final mediaQuery = MediaQuery.of(context);

    // Get the device's screen size
    final deviceWidth = mediaQuery.size.width;
    final deviceHeight = mediaQuery.size.height;

    // Get the device's orientation
    final isPortrait = mediaQuery.orientation == Orientation.portrait;

    // Get the device's pixel density
    final pixelRatio = mediaQuery.devicePixelRatio;

    // Use the MediaQuery data in your UI
    return Scaffold(
      appBar: AppBar(
        title: Text('My App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Device Width: ${deviceWidth}px'),
            Text('Device Height: ${deviceHeight}px'),
            Text('Orientation: ${isPortrait ? 'Portrait' : 'Landscape'}'),
            Text('Pixel Ratio: ${pixelRatio.toStringAsFixed(2)}'),
          ],
        ),
      ),
    );
  }
}
```

In the above example, we access the `MediaQuery` data by calling `MediaQuery.of(context)` within the build method of a widget. We then extract the relevant information such as the device's screen size, orientation, and pixel density.

By leveraging this information, you can create responsive layouts, adjust font sizes, and handle different aspect ratios in your Flutter app. `MediaQuery` is a powerful tool that helps make your app look great on various devices.

#flutter #mediaquery
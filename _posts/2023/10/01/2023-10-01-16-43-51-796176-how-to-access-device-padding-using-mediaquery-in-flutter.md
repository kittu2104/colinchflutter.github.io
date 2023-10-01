---
layout: post
title: "How to access device padding using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [flutter, mediaquery]
comments: true
share: true
---

When building a Flutter app, it's important to consider the different screen sizes and device orientations that your app will be running on. One aspect to take into account is the device padding, which includes the status bar, app bar, and system navigation bar.

To access device padding and ensure that your app's layout and user interface elements are properly aligned, you can use the `MediaQuery` class provided by Flutter.

Here's an example of how to use `MediaQuery` to access the device padding:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final padding = MediaQuery.of(context).padding;

    return MaterialApp(
      title: 'Device Padding Example',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Device Padding Example'),
        ),
        body: Container(
          padding: EdgeInsets.fromLTRB(
            padding.left,
            padding.top + kToolbarHeight,
            padding.right,
            padding.bottom,
          ),
          child: Center(
            child: Text(
              'Hello, Flutter!',
              style: TextStyle(fontSize: 24),
            ),
          ),
        ),
      ),
    );
  }
}
```

In the above code, we obtain the device padding by calling `MediaQuery.of(context).padding`. The `padding` object contains the distances from the screen edges to the useful content area of the device.

To ensure that the app's content is properly positioned, we use the obtained device padding to set the `padding` property of a `Container` widget. We update the `EdgeInsets` of the `Container` widget to accommodate the app bar using `kToolbarHeight`.

By utilizing `MediaQuery` and device padding, you can ensure that your app provides a consistent user experience across different devices and orientations.

#flutter #mediaquery
---
layout: post
title: "How to listen for platform brightness changes using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [flutter, mediaquery]
comments: true
share: true
---

In Flutter, you can use the `MediaQuery` class to listen for platform brightness changes. The `MediaQuery` class provides access to information about the current platform's screen and device characteristics, such as the brightness.

To listen for platform brightness changes, you can use the `mediaQuery` property provided by the `StatefulWidget` or `StatelessWidget` class. This property gives you access to the `MediaQueryData` object, which contains information about the current screen properties.

Here's an example code snippet to demonstrate how to listen for platform brightness changes:

```dart
import 'package:flutter/material.dart';

class BrightnessListener extends StatefulWidget {
  @override
  _BrightnessListenerState createState() => _BrightnessListenerState();
}

class _BrightnessListenerState extends State<BrightnessListener> {

  @override
  void initState() {
    super.initState();
    // Add a MediaQueryListener with a callback to handle brightness changes
    MediaQuery.of(context).addListener(_handleBrightnessChange);
  }

  @override
  void dispose() {
    // Remove the MediaQueryListener to avoid memory leaks
    MediaQuery.of(context).removeListener(_handleBrightnessChange);
    super.dispose();
  }

  void _handleBrightnessChange() {
    setState(() {
      // Handle the brightness change here
      // You can access the current brightness using `MediaQuery.of(context).platformBrightness`
      if (MediaQuery.of(context).platformBrightness == Brightness.light) {
        // Do something when the brightness changes to light
      } else {
        // Do something when the brightness changes to dark
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      // Build your UI here
    );
  }
}
```

In the above code, we create a `BrightnessListener` widget that extends `StatefulWidget`. Inside the `initState` method, we add a `MediaQueryListener` with a callback `_handleBrightnessChange` to handle the brightness changes.

In the `_handleBrightnessChange` method, we use the `platformBrightness` property of `MediaQueryData` to check if the brightness changes to light or dark. You can perform any specific actions or update the UI based on the brightness change.

Remember to remove the `MediaQueryListener` inside the `dispose` method to avoid memory leaks.

By implementing the above code, you can listen for platform brightness changes and adapt your app UI or behavior accordingly.

#flutter #mediaquery
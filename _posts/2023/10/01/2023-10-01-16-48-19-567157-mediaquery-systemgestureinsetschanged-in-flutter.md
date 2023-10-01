---
layout: post
title: "MediaQuery systemGestureInsetsChanged in Flutter"
description: " "
date: 2023-10-01
tags: [Flutter, MediaQuery]
comments: true
share: true
---

Flutter provides a rich set of widgets and APIs to build beautiful and responsive user interfaces. One such feature is `MediaQuery`, which allows you to access and respond to various information about the device's screen size, orientation, and various system configurations.

In this blog post, we will focus on the `systemGestureInsetsChanged` property of the `MediaQuery` class in Flutter. This property allows you to handle changes in the system gesture insets, which are the areas on the screen reserved for system gestures like the back button or swipe-up action.

## Understanding System Gesture Insets

System gesture insets are used to ensure that apps do not overlap with or obstruct the system gestures provided by the operating system. The insets vary depending on the device and platform. For example, on Android devices with navigation gestures, the system gesture insets would be different from those on iOS devices with a home indicator.

By utilizing the `systemGestureInsetsChanged` property, Flutter enables you to respond to changes in these insets and adjust your UI to provide a seamless user experience.

## Listening to System Gesture Insets Changes

To listen to changes in the system gesture insets, you can use the `MediaQuery.of(context).systemGestureInsetsChanged` callback. The `systemGestureInsets` property of the `MediaQueryData` provides information about the current system gesture insets.

Here's an example of how you can use this callback to update your UI when the system gesture insets change:

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  EdgeInsets _currentInsets = EdgeInsets.zero;

  @override
  void initState() {
    super.initState();
    WidgetsBinding.instance.addPostFrameCallback((_) {
      updateSystemGestureInsets();
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('System Gesture Insets'),
      ),
      body: Container(
        padding: _currentInsets, // Apply system gesture insets to your UI
        child: Center(
          child: Text(
            'Hello World',
            style: TextStyle(fontSize: 24.0),
          ),
        ),
      ),
    );
  }

  void updateSystemGestureInsets() {
    final data = MediaQuery.of(context);
    setState(() {
      _currentInsets = data.systemGestureInsets;
    });
  }
}
```

In this example, we create a simple `MyWidget` widget that listens to changes in the system gesture insets. We use the `addPostFrameCallback` method to ensure that the initial system gesture insets are updated after the first frame is painted. The `_currentInsets` variable stores the current system gesture insets, and we apply it to the `padding` property of the container to adjust the UI accordingly.

Remember to wrap your `MyWidget` widget with a `MaterialApp` or a `WidgetsApp` further up the widget tree to ensure that `MediaQuery` context is available.

## Conclusion

Understanding and responding to changes in the system gesture insets is crucial for creating a seamless user experience in your Flutter apps. By utilizing the `MediaQuery` class and its `systemGestureInsetsChanged` property, you can dynamically adjust your UI to accommodate different device configurations and system gestures.

Make sure to experiment with the `systemGestureInsetsChanged` callback in your Flutter projects and explore the various ways you can enhance your UI based on system gesture insets.

#Flutter #MediaQuery
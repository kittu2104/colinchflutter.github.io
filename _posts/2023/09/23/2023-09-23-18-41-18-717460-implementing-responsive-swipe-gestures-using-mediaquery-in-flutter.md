---
layout: post
title: "Implementing responsive swipe gestures using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [flutter, swipe]
comments: true
share: true
---

In Flutter, `MediaQuery` is a powerful and versatile class that allows us to retrieve information about the current device and screen dimensions. We can leverage this information to implement responsive swipe gestures that adapt to different screen sizes and orientations in our Flutter application.

## Setting up the Project

Before we dive into the implementation, make sure you have set up a Flutter project and have the necessary dependencies installed.

## Implementing Swipe Gestures

To implement swipe gestures, we will utilize the `GestureDetector` widget provided by Flutter. Here's an example code snippet demonstrating how to implement swipe gestures horizontally:

```dart
import 'package:flutter/material.dart';

class SwipeGesturePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Swipe Gesture Demo'),
      ),
      body: Center(
      child: Container(
        width: MediaQuery.of(context).size.width,
        height: MediaQuery.of(context).size.height,
        child: GestureDetector(
          onHorizontalDragEnd: (DragEndDetails details) {
            if (details.primaryVelocity! > 0) {
              // Swiped from left to right
              **// Perform custom action**
            } else {
              // Swiped from right to left
              **// Perform custom action**
            }
          },
          child: FlutterLogo(
            size: 200,
          ),
        ),
      ),
    ),
  );
  }
}
```

In this example, we wrap the `FlutterLogo` widget with a `GestureDetector`. The `onHorizontalDragEnd` callback is triggered when the user completes a horizontal swipe gesture. The `DragEndDetails` parameter contains information about the gesture, such as the velocity and direction.

Inside the callback, we can perform different actions based on the direction of the swipe. In the given example, we conditionally check the `primaryVelocity` value of `DragEndDetails` to determine the swipe direction. You can replace the comment lines with your custom actions.

## Conclusion

By utilizing `MediaQuery` and the `GestureDetector` widget, we can easily implement responsive swipe gestures in our Flutter applications. This allows for a more intuitive and user-friendly experience across different device sizes and orientations.

#flutter #swipe-gestures
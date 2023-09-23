---
layout: post
title: "Implementing responsive swipe gestures using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [flutter, responsiveUI]
comments: true
share: true
---

In today's mobile-first world, having a responsive user interface is crucial for creating a seamless user experience. One aspect of responsiveness is detecting swipe gestures on different screen sizes and adapting the app's behavior accordingly. In this blog post, we will explore how to implement responsive swipe gestures using `MediaQuery` in Flutter.

## What is MediaQuery?

`MediaQuery` is a Flutter class that allows you to retrieve information about the current device's screen size and other device-specific information. It provides access to properties such as device pixel ratio, orientation, and screen size, making it a powerful tool for building responsive UIs.

## Implementing Swipe Gesture Detection

To implement swipe gesture detection, we will use the `GestureDetector` widget provided by Flutter. The `GestureDetector` widget allows you to listen for and respond to different gestures like taps, swipes, and drags. We will wrap our widget tree with `GestureDetector` to capture swipe gestures on any part of the screen.

Here's an example of how to implement swipe gesture detection using `MediaQuery`:

```dart
import 'package:flutter/material.dart';

class SwipeGestureDetector extends StatelessWidget {
  final Widget child;
  final Function onSwipeLeft;
  final Function onSwipeRight;

  const SwipeGestureDetector({
    Key? key,
    required this.child,
    required this.onSwipeLeft,
    required this.onSwipeRight,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onHorizontalDragEnd: (DragEndDetails details) {
        final screenWidth = MediaQuery.of(context).size.width;
        final swipeThreshold = screenWidth / 4;

        if (details.primaryVelocity! > 0) {
          if (details.velocity.pixelsPerSecond.dx > swipeThreshold) {
            onSwipeRight();
          }
        } else {
          if (details.velocity.pixelsPerSecond.dx < -swipeThreshold) {
            onSwipeLeft();
          }
        }
      },
      child: child,
    );
  }
}
```

In the example above, we have created a `SwipeGestureDetector` widget that takes a `child` widget and callback functions `onSwipeLeft` and `onSwipeRight`. It listens for horizontal drag events and checks the velocity to determine if a swipe has occurred.

We also use `MediaQuery` to retrieve the screen width and calculate a swipe threshold. If the swipe velocity exceeds the threshold and the direction is either left or right, we call the respective callback function.

## Using the SwipeGestureDetector

To use the `SwipeGestureDetector`, simply wrap it around the part of the widget tree where you want to capture swipe gestures. Provide the `child` widget and the respective `onSwipeLeft` and `onSwipeRight` functions.

```dart
SwipeGestureDetector(
  onSwipeLeft: () {
    // Handle left swipe
  },
  onSwipeRight: () {
    // Handle right swipe
  },
  child: Container(
    color: Colors.white,
    child: Center(
      child: Text('Swipe Me!', style: TextStyle(fontSize: 24)),
    ),
  ),
),
```

In this example, we wrap a `Container` widget with a text label inside the `SwipeGestureDetector`. When the user swipes left or right on the `Container`, the respective callback functions will be invoked.

## Conclusion

By using `MediaQuery` in combination with the `GestureDetector` widget, we can easily implement responsive swipe gesture detection in Flutter. This allows us to create interactive and user-friendly experiences that adapt to different screen sizes and device orientations. Start implementing swipe gestures in your Flutter applications today and enhance the usability of your UI.

#flutter #responsiveUI
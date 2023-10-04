---
layout: post
title: "How to listen for system gesture inset changes using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [MediaQuery]
comments: true
share: true
---

Flutter provides a powerful way to handle system gesture inset changes using the `MediaQuery` widget. System gestures are the interactions that the user performs at the edges of the screen to trigger system-level functionality, such as opening the notification panel or navigating back.

In Flutter, system gesture insets represent the areas of the screen where system gestures can be detected. These insets can change dynamically based on the device and platform.

To listen for system gesture inset changes, you can use the `Padding` widget in combination with `MediaQuery`. Here's an example of how to do it:

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  EdgeInsets _systemGestureInsets = EdgeInsets.zero;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('System Gesture Insets'),
      ),
      body: Padding(
        padding: _systemGestureInsets,
        child: MediaQuery(
          data: MediaQuery.of(context).copyWith(
            // Update systemGestureInsets when they change
            padding: _systemGestureInsets,
          ),
          child: Builder(
            builder: (BuildContext context) {
              // Access systemGestureInsets using MediaQuery
              final EdgeInsets insets = MediaQuery.of(context).padding;

              // Update _systemGestureInsets when they change
              if (_systemGestureInsets != insets) {
                setState(() {
                  _systemGestureInsets = insets;
                });
              }

              // Build your UI here using the updated insets
              return Container(
                color: Colors.white,
                child: Center(
                  child: Text(
                    'Listening for System Gesture Insets',
                    style: TextStyle(
                      fontSize: 24.0,
                      fontWeight: FontWeight.bold,
                      color: Colors.black,
                    ),
                  ),
                ),
              );
            },
          ),
        ),
      ),
    );
  }
}
```

In this example, we create a `MyWidget` class that extends `StatefulWidget`. Inside the `build` method, we wrap our content with `Padding` widget and set its padding value to `_systemGestureInsets` which keeps track of the current system gesture insets.

Using `MediaQuery`, we can access the current system gesture insets through `MediaQuery.of(context).padding`. We update the insets and rebuild the UI whenever they change, ensuring that our layout adapts to the changes in system gesture insets.

By implementing this approach, you can effectively listen for system gesture inset changes in your Flutter app and handle them accordingly.

#Flutter #MediaQuery
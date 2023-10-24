---
layout: post
title: "CupertinoSwitch widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing a mobile application, it is essential to choose the appropriate UI components that match the platform's design guidelines. In Flutter, you have the freedom to choose between various widgets for building beautiful user interfaces. Two popular options are the `MaterialApp` and `CupertinoApp` widgets, each corresponding to the Material Design and Cupertino (iOS-style) design guidelines, respectively.

One commonly used widget in both Material Design and Cupertino is the `CupertinoSwitch`. This widget represents a toggle switch that can be used to switch between two options. However, the behavior and appearance of the `CupertinoSwitch` can differ depending on whether you use it within a `MaterialApp` or a `CupertinoApp`.

## CupertinoSwitch in MaterialApp
When used within a `MaterialApp`, the `CupertinoSwitch` widget will automatically adapt its appearance to match the Material Design style. It will be styled with the Material Design colors and animations, giving it a more platform-consistent look and feel on Android devices. 

To use the `CupertinoSwitch` within a `MaterialApp`, you can import the `material` package and include it in your Flutter code like this:

```dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Material Design App'),
        ),
        body: Center(
          child: CupertinoSwitch(
            value: true,
            onChanged: (newValue) {
              // Handle the switch state change
            },
          ),
        ),
      ),
    );
  }
}
```

## CupertinoSwitch in CupertinoApp
On the other hand, when used within a `CupertinoApp`, the `CupertinoSwitch` widget will adhere to the Cupertino (iOS) design guidelines. It will be styled with the familiar iOS-style colors, animation, and gestures. This ensures a consistent appearance on iOS devices and offers an experience that iOS users are accustomed to.

To use the `CupertinoSwitch` within a `CupertinoApp`, you need to import the `cupertino_icons` package and include it in your Flutter code like this:

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/cupertino_icons.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      home: CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          middle: Text('Cupertino Design App'),
        ),
        child: Center(
          child: CupertinoSwitch(
            value: true,
            onChanged: (newValue) {
              // Handle the switch state change
            },
          ),
        ),
      ),
    );
  }
}
```

By choosing the appropriate parent widget (`MaterialApp` or `CupertinoApp`) for your Flutter application, you can ensure that the `CupertinoSwitch` widget behaves and appears consistently with the design guidelines of the respective platform. This choice ultimately depends on your target platforms and the desired user experience for your app.

Remember to import the necessary packages (`material` for `MaterialApp`, and `cupertino` and `cupertino_icons` for `CupertinoApp`) to make the `CupertinoSwitch` widget available in your Flutter code.

#hashtags #flutter
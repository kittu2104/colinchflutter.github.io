---
layout: post
title: "Scaffold widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When building a cross-platform mobile application using Flutter, you have the option to use either the `MaterialApp` or the `CupertinoApp` widget as the root widget for your app. These widgets provide a consistent look and feel across platforms - Material Design for Android devices and Cupertino for iOS devices. One of the key widgets that you will frequently use in both `MaterialApp` and `CupertinoApp` is the `Scaffold` widget.

The `Scaffold` widget is a powerful and versatile widget that serves as a basic layout structure for your app. It provides features like app bars, navigation drawers, floating action buttons, and more. In this article, we will explore the similarities and differences in using the `Scaffold` widget with `MaterialApp` and `CupertinoApp`.

## MaterialApp

When using `MaterialApp`, the `Scaffold` widget follows Material Design guidelines and provides a set of widgets styled with Material Design elements. The `Scaffold` widget creates a layout with a top app bar, body, and bottom navigation.

Here's an example of using the `Scaffold` widget in a `MaterialApp`:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('My App'),
      ),
      body: Center(
        child: Text('Hello World'),
      ),
    ),
  ));
}
```

In this example, we have a `Scaffold` widget with an `AppBar` as the top app bar and a `Center` widget as the body.

## CupertinoApp

When using `CupertinoApp`, the `Scaffold` widget follows the iOS-style design guidelines. The `Scaffold` widget provides iOS-specific widgets like `CupertinoNavigationBar` and `CupertinoTabBar`, which are styled accordingly.

Here's an example of using the `Scaffold` widget in a `CupertinoApp`:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('My App'),
      ),
      child: Center(
        child: Text('Hello World'),
      ),
    ),
  ));
}
```

In this example, we have a `CupertinoPageScaffold` widget as the root widget, which is similar to the `Scaffold` widget in `MaterialApp`. It has a `CupertinoNavigationBar` as the top navigation bar and a `Center` widget as the body.

## Similarities and Differences

Both `MaterialApp` and `CupertinoApp` provide similar functionality through the `Scaffold` widget. However, the key difference lies in the visual appearance and the specific set of widgets used. 

- `MaterialApp` provides Material Design elements, such as `AppBar`, `FloatingActionButton`, and `MaterialButton`, while `CupertinoApp` provides iOS-specific widgets like `CupertinoNavigationBar`, `CupertinoTabBar`, and `CupertinoButton`.
- The styling and animation of these widgets will reflect the platform-specific design guidelines.

## Conclusion

Whether you choose to use `MaterialApp` or `CupertinoApp`, the `Scaffold` widget is a fundamental part of creating layout structures for your app. By using the appropriate `Scaffold` widgets for each platform, you can ensure a cohesive and platform-specific user experience in your Flutter application.

# References
- Scaffold Class - [Flutter Documentation](https://api.flutter.dev/flutter/material/Scaffold-class.html)
- CupertinoApp Class - [Flutter Documentation](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
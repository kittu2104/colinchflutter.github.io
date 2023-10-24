---
layout: post
title: "CupertinoPageRoute nested routing in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When it comes to building mobile applications with Flutter, you have two main options for handling nested routing: `MaterialApp` and `CupertinoApp`. Both provide navigation solutions, but they have some differences in terms of aesthetics and platform-specific features.

## MaterialApp

`MaterialApp` is the standard way of creating apps in Flutter and is optimized for Material Design. It offers a set of widgets and navigation components that provide a consistent look and feel across Android, iOS, and the web.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: MyApp(),
    routes: {
      '/details': (context) => DetailsPage(),
      '/settings': (context) => SettingsPage(),
    },
  ));
}
```

To enable nested routing using `MaterialApp`, you can define your routes using the `routes` property. Each route is associated with a specific widget that will be displayed when the route is navigated to.

```dart
Navigator.pushNamed(context, '/details');
```

With `MaterialApp`, you have access to material-specific design elements such as `AppBar`, `Drawer`, and `FloatingActionButton`. These widgets can be used to create a consistent Material Design experience across your app.

## CupertinoApp

`CupertinoApp`, on the other hand, is designed specifically for iOS-style apps, following the Apple Human Interface Guidelines. It has a different set of widgets and navigation components optimized for iOS aesthetics and interactions.

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: MyApp(),
    routes: {
      '/details': (context) => DetailsPage(),
      '/settings': (context) => SettingsPage(),
    },
  ));
}
```

Similar to `MaterialApp`, `CupertinoApp` allows you to define routes using the `routes` property. When navigating to a specific route, the associated widget will be displayed.

```dart
Navigator.pushNamed(context, '/details');
```

With `CupertinoApp`, you can leverage iOS-specific design elements like the `CupertinoNavigationBar`, `CupertinoTabBar`, and `CupertinoButton` to create an app that blends seamlessly with the iOS ecosystem.

## Choosing between MaterialApp and CupertinoApp

Your choice between `MaterialApp` and `CupertinoApp` depends on the visual style and user experience you want to achieve. If you're targeting both Android and iOS and prefer the Material Design aesthetic, `MaterialApp` is a good choice. On the other hand, if you're building an iOS-specific app that follows the iOS design principles, `CupertinoApp` is the way to go.

It's important to note that although `CupertinoApp` is optimized for iOS, Flutter's framework allows you to create platform-specific designs even when using `MaterialApp`. So, if you prefer the iOS design but want to target multiple platforms, you can still achieve a similar look and feel using `MaterialApp` and the Cupertino-style design elements available in the Flutter framework.

# References
- [Flutter Documentation - MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [Flutter Documentation - CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
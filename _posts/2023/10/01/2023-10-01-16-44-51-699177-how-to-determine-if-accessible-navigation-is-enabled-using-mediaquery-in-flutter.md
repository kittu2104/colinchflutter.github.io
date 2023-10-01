---
layout: post
title: "How to determine if accessible navigation is enabled using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

To determine if accessible navigation is enabled, you can check the `accessibleNavigationFocusMode` property of `MediaQueryData`. Here's an example code snippet:

```dart
import 'package:flutter/material.dart';

bool isAccessibleNavigationEnabled(BuildContext context) {
  final MediaQueryData mediaQueryData = MediaQuery.of(context);
  return mediaQueryData.accessibleNavigationFocusMode ==
      MediaQueryAccessibleNavigationFocusMode.auto;
}

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    bool accessibleNavigationEnabled = isAccessibleNavigationEnabled(context);
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Accessible Navigation'),
        ),
        body: Center(
          child: Text(
            accessibleNavigationEnabled
                ? 'Accessible Navigation is enabled'
                : 'Accessible Navigation is disabled',
            style: TextStyle(fontSize: 20),
          ),
        ),
      ),
    );
  }
}
```

In the above code, the `isAccessibleNavigationEnabled` function checks if the `accessibleNavigationFocusMode` property is set to `auto`, which indicates that accessible navigation is enabled. It returns `true` if accessible navigation is enabled, and `false` otherwise.

In the `MyApp` widget, the `accessibleNavigationEnabled` variable is used to display a message indicating whether accessible navigation is enabled or disabled.

Remember to import the necessary Flutter packages and adjust the UI according to your needs.
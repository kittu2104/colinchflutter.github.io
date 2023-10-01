---
layout: post
title: "MediaQuery highContrast in Flutter"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

Flutter is a cross-platform framework for building native mobile apps using a single codebase. It offers a wide range of features and utilities to make app development easier and more efficient. One such feature is the `MediaQuery` class, which provides access to various information about the app's environment.

Among the properties provided by `MediaQuery`, there is a property called `highContrast`. This property indicates whether the user has enabled a high contrast mode on their device. High contrast mode is commonly used by people with visual impairments to enhance the visibility of content on the screen.

When `highContrast` is `true`, it means that the app is being viewed in high contrast mode. By detecting this property, you can adapt your app's UI to provide a better experience for users with visual impairments.

To use `MediaQuery.highContrast`, you first need to obtain the `MediaQueryData` for your app. This can be done by calling `MediaQuery.of(context)`, where `context` is the `BuildContext` of your app. Once you have the `MediaQueryData`, you can access the `highContrast` property.

Here's an example code snippet that demonstrates how to use `MediaQuery.highContrast` in Flutter:

```dart
import 'package:flutter/material.dart';

class HighContrastExampleApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final mediaQueryData = MediaQuery.of(context);
    final isHighContrast = mediaQueryData.highContrast;

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('High Contrast Example'),
        ),
        body: Center(
          child: Text(
            isHighContrast ? 'High Contrast Mode Enabled' : 'High Contrast Mode Disabled',
            style: TextStyle(
              color: isHighContrast ? Colors.white : Colors.black,
              fontSize: 18.0,
              fontWeight: FontWeight.bold,
            ),
          ),
        ),
      ),
    );
  }
}
```

In the above example, we are checking the value of `isHighContrast` obtained from `MediaQuery.highContrast` and displaying a different message based on whether high contrast mode is enabled or disabled. We are also adjusting the text color based on the mode to ensure proper visibility.

Remember to import the necessary dependencies and wrap your app with a `MaterialApp` widget for the example to work.

By utilizing `MediaQuery.highContrast`, you can create more inclusive and accessible apps by adapting your UI to accommodate users in high contrast mode.
---
layout: post
title: "How to use `MediaQuery` in Flutter for responsive UI design"
description: " "
date: 2023-09-23
tags: [flutter, responsiveui]
comments: true
share: true
---

In Flutter, `MediaQuery` is a powerful widget that allows you to create responsive user interfaces. It provides information about the current device's size, orientation, and other properties. By utilizing `MediaQuery`, you can build layouts that adapt to different screen sizes, ensuring your app looks great on various devices.

Here's a step-by-step guide on how to use `MediaQuery` in Flutter to create a responsive UI design:

## Step 1: Import the necessary package

To use `MediaQuery`, you need to import the `flutter` package in your Dart file:

```dart
import 'package:flutter/material.dart';
```

## Step 2: Wrap your root widget with `MaterialApp`

To access the `MediaQuery` data, you need to wrap your root widget with the `MaterialApp` widget. This widget provides the necessary context for `MediaQuery` to work correctly:

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive App',
      home: HomePage(),
    );
  }
}
```

## Step 3: Access `MediaQuery` data

To access `MediaQuery` data, you can use the `MediaQuery.of(context)` method. It returns a `MediaQueryData` object, which contains information about the device's screen size and orientation:

```dart
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final mediaQuery = MediaQuery.of(context);
    final screenWidth = mediaQuery.size.width;
    final screenHeight = mediaQuery.size.height;
    // Additional properties available: devicePixelRatio, textScaleFactor, etc.

    return Container(
      width: screenWidth * 0.8, // Example usage: responsive width
      height: screenHeight * 0.5, // Example usage: responsive height
      child: Text('Responsive UI'),
    );
  }
}
```

In the above code, we access the `MediaQueryData` using `MediaQuery.of(context)`. We then extract the screen width and height using `mediaQuery.size.width` and `mediaQuery.size.height` respectively. You can use these values to make your UI components dynamically adjust to the available screen space.

## Step 4: Update UI accordingly

With the `MediaQuery` data, you can now update your UI components based on the device's screen size. For example, you can conditionally show or hide certain widgets, adjust font sizes, or dynamically set component dimensions.

```dart
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final mediaQuery = MediaQuery.of(context);
    final screenWidth = mediaQuery.size.width;
    final screenHeight = mediaQuery.size.height;

    return Container(
      width: screenWidth * 0.8, // Example usage: responsive width
      height: screenHeight * 0.5, // Example usage: responsive height
      child: Column(
        children: <Widget>[
          if (screenWidth > 600) // Show widget for larger screens
            Text('Larger Screen Widget'),
          Text('Common Widget'),
          if (mediaQuery.orientation == Orientation.portrait) // Show widget in portrait mode
            Text('Portrait Widget'),
        ],
      ),
    );
  }
}
```

In the above code, we conditionally show different widgets based on the screen width and orientation. We use the `if` statement to check conditions and render the appropriate widgets.

## Conclusion

By utilizing `MediaQuery` in Flutter, you can create responsive UI designs that adapt to different devices. Whether it's adjusting widget sizes, nesting widgets conditionally, or changing font sizes, `MediaQuery` helps you create a consistent and user-friendly user interface across various screen sizes. Start using `MediaQuery` today and ensure your app looks great on every device!

#flutter #responsiveui
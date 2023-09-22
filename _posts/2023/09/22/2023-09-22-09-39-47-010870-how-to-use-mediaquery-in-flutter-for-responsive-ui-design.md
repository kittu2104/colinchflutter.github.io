---
layout: post
title: "How to use `MediaQuery` in Flutter for responsive UI design"
description: " "
date: 2023-09-22
tags: [flutter, responsiveUI]
comments: true
share: true
---

Creating responsive user interfaces (UI) is a crucial aspect of mobile app development. In Flutter, the `MediaQuery` class allows developers to build responsive layouts that adapt to different device sizes and orientations. In this blog post, we will explore how to utilize `MediaQuery` in Flutter for responsive UI design.

## What is `MediaQuery`?

`MediaQuery` is a class in the Flutter framework that provides information about the current device or app context. It allows developers to access properties such as screen size, device pixel density, orientation, and more. By leveraging this information, we can build UIs that dynamically adjust and adapt to various devices.

## Getting Started

To begin using `MediaQuery` in your Flutter app, follow these steps:

1. Import the `material.dart` package:

```dart
import 'package:flutter/material.dart';
```

2. Access the `MediaQuery` instance using `MediaQuery.of(context)`.

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var mediaQuery = MediaQuery.of(context);
    // ...
  }
}
```

## Utilizing `MediaQuery` Properties

`MediaQuery` provides various properties that can be used to create responsive UIs. Here are a few examples:

### Screen Size

You can obtain the screen size using the `mediaQuery.size` property. This returns a `Size` object that contains the available width and height of the screen.

```dart
var screenSize = mediaQuery.size;
var screenWidth = screenSize.width;
var screenHeight = screenSize.height;
```

### Device Pixel Density

To accommodate screens with different pixel densities, you can use the `mediaQuery.devicePixelRatio` property. This value represents the ratio of logical pixels to physical pixels on the screen.

```dart
var devicePixelRatio = mediaQuery.devicePixelRatio;
```

### Orientation

You can determine the current screen orientation using the `mediaQuery.orientation` property, which returns `Orientation.portrait` or `Orientation.landscape`.

```dart
var orientation = mediaQuery.orientation;
if (orientation == Orientation.portrait) {
  // Adjust UI for portrait orientation
} else {
  // Adjust UI for landscape orientation
}
```

### Padding and Insets

To account for system UI elements like the status bar or bottom navigation bar, the `mediaQuery.padding` and `mediaQuery.viewInsets` properties can be used to retrieve the space occupied by these elements.

```dart
var statusBarHeight = mediaQuery.padding.top;
var bottomNavigationBarHeight = mediaQuery.viewInsets.bottom;
```

## Building Responsive UI with `MediaQuery`

Now that we have access to the `MediaQuery` properties, we can use them to create responsive UIs. Here's a simple example that demonstrates how to adjust the UI based on the screen width:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var mediaQuery = MediaQuery.of(context);
    var screenWidth = mediaQuery.size.width;

    return Scaffold(
      body: Container(
        width: (screenWidth > 600) ? 400 : double.infinity,
        height: 200,
        color: Colors.blue,
        child: Center(
          child: Text(
            'Responsive Text',
            style: TextStyle(
              fontSize: (screenWidth > 600) ? 24 : 16,
              color: Colors.white,
            ),
          ),
        ),
      ),
    );
  }
}
```

In the above example, the width of the `Container` widget is set to 400 pixels if the screen width is greater than 600 pixels; otherwise, it takes the full available width. Additionally, the font size of the text adjusts based on the screen width.

By utilizing `MediaQuery`, we can create UIs that adapt to different screen sizes, pixel densities, orientations, and other device-specific properties.

## Conclusion

Developing responsive UIs is essential for creating great user experiences across a variety of devices. Flutter's `MediaQuery` class provides developers with vital information about the device, enabling them to build interfaces that dynamically adapt to different contexts. By leveraging `MediaQuery` properties, such as screen size, pixel density, and orientation, we can effortlessly create responsive UI designs in Flutter. So, go ahead and utilize `MediaQuery` to create stunning and adaptable UIs for your Flutter apps!

#flutter #responsiveUI #MediaQuery
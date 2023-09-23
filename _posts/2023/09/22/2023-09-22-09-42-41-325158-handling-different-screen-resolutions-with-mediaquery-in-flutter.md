---
layout: post
title: "Handling different screen resolutions with `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: []
comments: true
share: true
---

Here's an example of how you can use `MediaQuery` to handle different screen resolutions in Flutter:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Retrieve the current MediaQueryData object
    final mediaQuery = MediaQuery.of(context);

    // Get the device's screen width and height
    final screenWidth = mediaQuery.size.width;
    final screenHeight = mediaQuery.size.height;

    // Get the device's pixel density
    final screenDensity = mediaQuery.devicePixelRatio;

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Screen Resolutions'),
        ),
        body: Container(
          child: Center(
            child: Text(
              'Screen Width: ${screenWidth.toStringAsFixed(2)},'
              'Screen Height: ${screenHeight.toStringAsFixed(2)},'
              'Pixel Density: ${screenDensity.toStringAsFixed(2)}',
              style: TextStyle(fontSize: 20.0),
            ),
          ),
        ),
      ),
    );
  }
}
```

In the example above, we retrieve the `MediaQueryData` object by calling `MediaQuery.of(context)`. We then extract the screen width, height, and pixel density from the `mediaQuery` object. We can use these values to create responsive layouts and render content correctly.

By using the `MediaQuery` class, you can adjust your app's layout, fonts, images, and other elements based on the device's screen resolution. It allows you to provide an optimal user experience across a wide range of devices and screen sizes.

Remember to test your app on various devices and screen resolutions to ensure that it looks and functions as intended.
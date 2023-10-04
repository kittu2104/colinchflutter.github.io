---
layout: post
title: "MediaQuery platformBrightness in Flutter"
description: " "
date: 2023-10-01
tags: [MediaQuery]
comments: true
share: true
---

Flutter is a popular cross-platform framework for building beautiful and engaging user interfaces. One of the many features it provides is the `MediaQuery` class, which allows us to access various information about the device such as screen size, orientation, and brightness. In this blog post, we'll focus on using the `platformBrightness` property of `MediaQuery` to dynamically adapt our app's UI based on the device's brightness mode.

## What is `platformBrightness`?

The `platformBrightness` property is a part of the `MediaQueryData` class in Flutter. It represents the current brightness mode of the device's operating system. The brightness can be either `Brightness.light` or `Brightness.dark`, depending on the system settings or the user's preference.

## Why use `platformBrightness`?

By leveraging the `platformBrightness` property, we can adjust the appearance of our app to match the device's brightness mode. This can help improve the user experience and make our app feel more native on different devices. For example, we can use a light color scheme when the device is in light mode and switch to a dark color scheme in dark mode.

## How to use `platformBrightness`?

To access the `platformBrightness` property, we first need to obtain the `MediaQueryData` object using the `MediaQuery.of()` method. Once we have the `MediaQueryData`, we can use the `platformBrightness` property to determine the current brightness mode of the device.

Here's an example of how to use `platformBrightness` in Flutter:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final brightness = MediaQuery.of(context).platformBrightness;
    final isDarkMode = brightness == Brightness.dark;

    return MaterialApp(
      title: 'Brightness Example',
      theme: isDarkMode ? ThemeData.dark() : ThemeData.light(),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Brightness Example'),
      ),
      body: Container(
        child: Center(
          child: Text(
            'Welcome to my app!',
            style: TextStyle(
              fontSize: 20.0,
              fontWeight: FontWeight.bold,
              color: Colors.blue,
            ),
          ),
        ),
      ),
    );
  }
}
```

In the example above, we retrieve the `brightness` using `MediaQuery.of(context).platformBrightness` and then determine if the device is in dark mode. We then apply the corresponding theme using `ThemeData.dark()` or `ThemeData.light()`. This ensures that the app adapts to the device's brightness mode.

## Conclusion

By utilizing the `platformBrightness` property of `MediaQuery` in Flutter, we can create apps that adapt to the device's brightness mode. This improves the user experience and makes our app feel more consistent with the device's native interface. So, next time you're designing a Flutter app, consider using `platformBrightness` to enhance its adaptability! #Flutter #MediaQuery
---
layout: post
title: "MediaQuery platformBrightnessChanged in Flutter"
description: " "
date: 2023-10-01
tags: [MediaQuery]
comments: true
share: true
---

Flutter provides a powerful set of widgets and features for developing cross-platform mobile apps. One of the useful features is the MediaQuery widget, which allows developers to access information about the device's screen or layout constraints. In this blog post, we will explore the `platformBrightnessChanged` property of the MediaQuery widget in Flutter.

## What is `platformBrightnessChanged`?

The `platformBrightnessChanged` property is a callback provided by MediaQuery that allows developers to handle changes in the brightness of the platform. This can be useful when you want to adjust the appearance of your app based on the system-wide brightness settings.

## Using `platformBrightnessChanged`

To use the `platformBrightnessChanged` callback, start by wrapping your app or a specific part of your app with a MediaQuery widget. Then, pass a function to the `platformBrightnessChanged` property to handle the callback.

Here's an example of how you can use `platformBrightnessChanged` to update the theme of your app based on the system brightness:

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData.light(),
      darkTheme: ThemeData.dark(),
      home: MediaQuery(
        data: MediaQueryData(),
        child: MyHomePage(),
        platformBrightnessChanged: (Brightness brightness) {
          // Handle brightness change here
          if (brightness == Brightness.light) {
            // Update the app theme to light mode
          } else {
            // Update the app theme to dark mode
          }
        },
      ),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Platform Brightness Example'),
      ),
      body: ...
    );
  }
}
```

In the above example, we define a `platformBrightnessChanged` callback that updates the app theme based on the brightness value passed. If the brightness is `Brightness.light`, we update the app theme to use a light theme, and if it's `Brightness.dark`, we update the theme to a dark mode.

By using the `platformBrightnessChanged` callback, your app will automatically reflect any changes in the system's brightness settings.

## Conclusion

The `platformBrightnessChanged` property of the MediaQuery widget in Flutter provides a convenient way to handle changes in the system-wide brightness settings. By leveraging this callback, you can dynamically update the appearance of your app based on the user's brightness preferences. This makes your app more user-friendly and adaptable to different lighting conditions.

By understanding and utilizing the power of MediaQuery, you can create better user experiences in your Flutter apps.

#Flutter #MediaQuery
---
layout: post
title: "MediaQuery platformBrightness in Flutter"
description: " "
date: 2023-10-01
tags: [MediaQuery, platformBrightness]
comments: true
share: true
---

In Flutter, the `MediaQuery` class provides access to the current platform's display and design information. One useful property is `platformBrightness`, which can help you determine the brightness mode of the device's operating system.

## What is platformBrightness?

`platformBrightness` is a property of the `MediaQueryData` class that represents the brightness mode of the device's operating system. It can have two possible values:

- `Brightness.light`: Indicates that the device is set to light mode.
- `Brightness.dark`: Indicates that the device is set to dark mode.

By leveraging `platformBrightness`, you can customize your app's behavior or appearance based on the user's system brightness mode.

## How to use platformBrightness?

To access the `platformBrightness`, you'll need to first obtain the `MediaQueryData` instance from the current `BuildContext`. This can be done using the `MediaQuery.of(context)` method.

Here's an example of how you can use `platformBrightness` to change the theme of your Flutter app:

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
      title: 'My App',
      theme: ThemeData(
        brightness: isDarkMode ? Brightness.dark : Brightness.light,
        // Customize your theme based on the brightness mode
        // ...
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My Page'),
      ),
      body: Center(
        child: Text(
          'Hello, Flutter!',
          style: TextStyle(
            fontSize: 20,
            fontWeight: FontWeight.bold,
            color: Theme.of(context).textTheme.bodyText1.color,
            // Customize the text color based on the brightness mode
          ),
        ),
      ),
    );
  }
}
```

In the above example, we use the `platformBrightness` value to determine whether the system is in dark mode or light mode. We then set the theme's brightness and customize the various components accordingly.

## Conclusion

By utilizing `MediaQuery`'s `platformBrightness` property in Flutter, you can easily adapt your app's appearance and behavior based on the user's preferred system brightness mode. This feature is particularly useful for providing a consistent and engaging user experience across different devices and user preferences.

#Flutter #MediaQuery #platformBrightness
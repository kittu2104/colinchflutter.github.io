---
layout: post
title: "Enabling dark mode in MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In this blog post, we will learn how to enable dark mode in a Flutter application using the MaterialApp widget. Dark mode has become increasingly popular as it reduces eye strain and saves battery life on devices with OLED screens.

## Table of Contents
- [What is MaterialApp](#what-is-materialapp)
- [Enabling Dark Mode](#enabling-dark-mode)
- [Conclusion](#conclusion)
- [References](#references)

## What is MaterialApp

MaterialApp is a core Flutter widget that implements the Material Design in your application. It provides a range of features and configurations to customize the overall look and feel of the app, such as themes, navigation, and internationalization.

## Enabling Dark Mode

To enable dark mode in your MaterialApp, you need to make use of the `theme` property. The theme property accepts a ThemeData object, which allows us to customize the visual styling of our app.

Here's an example of how to enable dark mode by setting the ThemeData's `brightness` property to `Brightness.dark`:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(
    MaterialApp(
      theme: ThemeData(
        brightness: Brightness.dark,
      ),
      home: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Dark Mode Enabled'),
      ),
      body: Center(
        child: Text(
          'Welcome to Dark Mode!',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

In the above example, we set the `brightness` property of the ThemeData to `Brightness.dark` inside the theme object. This turns the overall app interface to dark mode.

You can further customize the dark mode by modifying other properties within the ThemeData object, such as text color, background color, and more. The ThemeData class provides numerous options to help you achieve the desired dark mode appearance.

## Conclusion

Enabling dark mode in your MaterialApp is a great way to enhance the user experience and offer a more visually appealing interface. By leveraging the flexibility of the ThemeData class, you can customize various aspects of the dark mode to match your app's design.

Dark mode is particularly useful for apps that are used in low-light environments or for users who prefer a darker color scheme. With Flutter, implementing dark mode is straightforward and can greatly improve the overall user experience.

## References

- [MaterialApp class documentation](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [ThemeData class documentation](https://api.flutter.dev/flutter/material/ThemeData-class.html)
- [Implementing dark mode in Flutter](https://flutter.dev/docs/cookbook/design/dark-mode)
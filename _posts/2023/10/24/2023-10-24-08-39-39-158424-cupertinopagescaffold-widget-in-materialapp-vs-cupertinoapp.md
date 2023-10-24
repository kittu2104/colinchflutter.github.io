---
layout: post
title: "CupertinoPageScaffold widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [materialdesign]
comments: true
share: true
---

When developing a Flutter application, you have the option to choose between MaterialApp and CupertinoApp as the root widget for your app. Each of these widgets provides a different look and feel based on the platform your app runs on - Material Design for Android and iOS-like design for iOS.

In this blog post, we will focus on comparing the CupertinoPageScaffold widget used in MaterialApp and CupertinoApp, and how they differ in terms of functionality and appearance.

## MaterialApp
MaterialApp is the most commonly used root widget for building apps in Flutter. It provides a Material Design-themed app experience for Android devices, using components like MaterialApp, Scaffold, AppBar, etc.

When using MaterialApp, you can use the Scaffold widget to create a screen or a page within your app. Scaffold provides a layout structure to build your UI with different components like AppBar, BottomNavigationBar, FloatingActionButton, and more.

## CupertinoApp
CupertinoApp, on the other hand, is used to create an iOS-like app experience. It provides a Cupertino design-themed look for iOS devices, which includes components like CupertinoAppBar, CupertinoTabBar, and others.

To create a screen or a page within a CupertinoApp, you can use the CupertinoPageScaffold widget. It provides a layout structure similar to the Scaffold widget in MaterialApp, but with a Cupertino design.

## CupertinoPageScaffold
CupertinoPageScaffold is a widget that provides a basic page structure for your app's screens using the Cupertino design. It includes a navigation bar at the top, a content area, and an optional bottom area.

The CupertinoPageScaffold widget accepts three main parameters:
- `navigationBar`: This parameter allows you to specify the navigation bar widget for the page. By default, it is positioned at the top of the screen.
- `child`: This is the main content of the page, typically a SingleChildScrollView or a ListView widget.
- `bottomNavigationBar`: This parameter allows you to specify a bottom navigation bar widget for the page.

## Usage in MaterialApp and CupertinoApp
To use the CupertinoPageScaffold widget with MaterialApp, you need to wrap it inside a Scaffold widget. This is because MaterialApp is designed to work with the Material Design components provided by Flutter.

On the other hand, when using CupertinoApp, you can directly use the CupertinoPageScaffold widget without wrapping it inside a Scaffold.

```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('MaterialApp with CupertinoPageScaffold'),
      ),
      body: CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          middle: Text('CupertinoPageScaffold'),
        ),
        child: Center(
          child: Text('Hello World!'),
        ),
      ),
    ),
  ));
}
```

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('CupertinoPageScaffold'),
      ),
      child: Center(
        child: Text('Hello World!'),
      ),
    ),
  ));
}
```

## Conclusion
In conclusion, the CupertinoPageScaffold widget provides a basic page structure for building iOS-like experiences in both MaterialApp and CupertinoApp. While MaterialApp is primarily used for Material Design-themed apps on Android, CupertinoApp offers an iOS-like design for iOS devices.

Understanding the differences between these two root widgets helps in making an informed decision when developing cross-platform Flutter applications. Remember to refer to the Flutter documentation for more information and to further explore the available widgets and their functionalities.

#flutter #materialdesign
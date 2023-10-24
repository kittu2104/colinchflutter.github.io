---
layout: post
title: "Widget tree structure in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [materialdesign, cupertino]
comments: true
share: true
---

When developing mobile applications with Flutter, you can choose between two different themes: Material Design and Cupertino. Flutter provides two main widgets, MaterialApp and CupertinoApp, to define the theme and structure the widget tree accordingly.

## MaterialApp

**MaterialApp** is the widget that sets up a Material Design theme for your app. It provides a set of predefined widgets that follow the Material Design guidelines, such as AppBar, FloatingActionButton, and BottomNavigationBar. 

To create a **MaterialApp**, you can use the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(
    MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('My App'),
        ),
        body: Center(
          child: Text('Hello, World!'),
        ),
      ),
    ),
  );
}
```

In this example, the **MaterialApp** is the root widget, which contains a **Scaffold** widget that defines the overall structure of the screen. You can customize the app bar, body, and other elements according to your requirements.

## CupertinoApp

**CupertinoApp** is the widget that sets up a Cupertino Design theme for your app. It provides a set of iOS-specific widgets that follow the Cupertino design language, such as CupertinoNavigationBar, CupertinoButton, and CupertinoPageScaffold.

To create a **CupertinoApp**, you can use the following code:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(
    CupertinoApp(
      home: CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          middle: Text('My App'),
        ),
        child: Center(
          child: Text('Hello, World!'),
        ),
      ),
    ),
  );
}
```

In this example, the **CupertinoApp** is the root widget, which contains a **CupertinoPageScaffold** widget that defines the overall structure of the screen. You can customize the navigation bar, child widget, and other elements as needed.

## Choosing Between MaterialApp and CupertinoApp

Whether to use MaterialApp or CupertinoApp depends on the platform you are targeting and the design language you want to follow. 

- If you're building an app for Android or prefer the Material Design look, use the **MaterialApp** and its associated widgets.
- If you're building an app for iOS or prefer the Cupertino design language, use the **CupertinoApp** and its associated widgets.

Remember to consider the platform guidelines and user experience expectations when making your choice.

Make sure to import the appropriate packages for **MaterialApp** (`flutter/material.dart`) and **CupertinoApp** (`flutter/cupertino.dart`) in your Dart file.

For more information, you can refer to the official documentation:

- [MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)

#flutter #materialdesign #cupertino
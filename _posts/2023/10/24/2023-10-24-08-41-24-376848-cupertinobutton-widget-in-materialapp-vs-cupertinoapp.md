---
layout: post
title: "CupertinoButton widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In Flutter, the CupertinoButton widget is a button styled according to the iOS design guidelines. It is used to create buttons with a sleek, minimalistic look similar to those found in iOS apps.

When it comes to using the CupertinoButton widget, you have two main options: incorporating it within a MaterialApp or using it directly within a CupertinoApp.

## MaterialApp

The MaterialApp widget is the entry point for a Flutter app that follows the Material Design guidelines, which are primarily used for Android apps. However, the MaterialApp widget also provides a convenient way to include Cupertino-style widgets, such as the CupertinoButton, in your app.

To use the CupertinoButton widget within a MaterialApp, you need to import the cupertino_icons package and set the theme property of MaterialApp to a CupertinoThemeData.

Here is an example of using the CupertinoButton within MaterialApp:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';
import 'package:flutter/cupertino_icons.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(
        cupertinoOverrideTheme: CupertinoThemeData(
          // Set the button's default textStyle
          textTheme: CupertinoTextThemeData(
            textStyle: TextStyle(color: Colors.white),
          ),
        ),
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('CupertinoButton in MaterialApp'),
        ),
        body: Center(
          child: CupertinoButton(
            child: Text('Press me'),
            onPressed: () {
              // Handle button press
            },
          ),
        ),
      ),
    );
  }
}
```

## CupertinoApp

On the other hand, if you want to exclusively build an app with Cupertino-style widgets, you can use the CupertinoApp widget as the entry point for your app. This widget sets up the app's layout and provides access to Cupertino-style widgets, including the CupertinoButton.

To use the CupertinoButton widget within a CupertinoApp, you need to import the cupertino_icons package and wrap the CupertinoButton with the MaterialApp's child property.

Here is an example of using the CupertinoButton within a CupertinoApp:

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/cupertino_icons.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      home: CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          middle: Text('CupertinoButton in CupertinoApp'),
        ),
        child: Center(
          child: CupertinoButton(
            child: Text('Press me'),
            onPressed: () {
              // Handle button press
            },
          ),
        ),
      ),
    );
  }
}
```

## Conclusion

In conclusion, both MaterialApp and CupertinoApp allow you to use the CupertinoButton widget in your Flutter app. The choice between the two depends on whether you want to build an app following the Material Design guidelines or exclusively create an iOS-styled app. Choose the one that aligns with your design preferences and target platform.
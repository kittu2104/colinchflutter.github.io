---
layout: post
title: "CupertinoPageRoute route builder in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [userinterface]
comments: true
share: true
---

When building a Flutter application, you have the option to use either the `CupertinoPageRoute` with `CupertinoApp` or the `MaterialPageRoute` with `MaterialApp` for your routing needs. Both options provide navigation functionalities, but there are some differences to consider.

## CupertinoPageRoute with CupertinoApp

The `CupertinoPageRoute` is specifically designed for iOS-style navigation experiences, following Apple's Human Interface Guidelines. It provides a native-looking transition between screens, with features such as iOS-style page transitions and Cupertino-themed navigation bars.

To use `CupertinoPageRoute`, you need to wrap your app with a `CupertinoApp` widget. For example:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: MyApp(),
  ));
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        title: Text('My App'),
      ),
      child: Center(
        child: Text('Welcome to MyApp'),
      ),
    );
  }
}
```

In this example, we wrap our app with `CupertinoApp` and use `CupertinoPageScaffold` for the main content. The `CupertinoNavigationBar` provides the iOS-style navigation bar.

## MaterialPageRoute with MaterialApp

On the other hand, `MaterialPageRoute` is the default route builder in Flutter and is primarily designed for Material Design-based applications. It offers features like page transitions using material design principles and a material-themed navigation bar.

To use `MaterialPageRoute`, you need to wrap your app with a `MaterialApp` widget. For example:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: MyApp(),
  ));
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My App'),
      ),
      body: Center(
        child: Text('Welcome to MyApp'),
      ),
    );
  }
}
```

In this example, we wrap our app with `MaterialApp` and use `Scaffold` for the main content. The `AppBar` provides the material-themed navigation bar.

## Choosing between CupertinoPageRoute and MaterialPageRoute

The choice between `CupertinoPageRoute` and `MaterialPageRoute` depends on the visual style and experience you want to achieve in your app. If you are developing an app specifically for iOS or want an iOS-like user interface, you should use `CupertinoPageRoute` and `CupertinoApp`. Conversely, if you want a material-themed user interface that works well across different platforms, `MaterialPageRoute` and `MaterialApp` are the way to go.

Remember to import the necessary packages (`cupertino.dart` for `CupertinoPageRoute` and `material.dart` for `MaterialPageRoute`) before using them.

Overall, both approaches provide navigation capabilities and enable you to build immersive app experiences. Choose the one that aligns best with your desired style and functionality!

[#flutter](flutter) [#userinterface](userinterface)
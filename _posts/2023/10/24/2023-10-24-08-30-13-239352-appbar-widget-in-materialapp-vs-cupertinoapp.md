---
layout: post
title: "Appbar widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [appbar]
comments: true
share: true
---

When building a mobile application, one of the key components is the app bar or navigation bar. In Flutter, there are two different ways to implement an app bar: using the `AppBar` widget in `MaterialApp` or using the `CupertinoNavigationBar` in `CupertinoApp`. 

## Using AppBar in MaterialApp

The `AppBar` widget is part of `MaterialApp` and follows the Material Design guidelines. It provides a consistent and familiar look for Android users. To use `AppBar`, simply include it as the `AppBar` property within the `Scaffold` widget.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('My App'),
      ),
      // Other content of your app
    ),
  ));
}
```

This code snippet demonstrates the usage of `AppBar` within a `MaterialApp`. It sets the title of the AppBar as "My App". You can also customize other properties of the `AppBar`, such as background color, actions, and leading widgets.

## Using CupertinoNavigationBar in CupertinoApp

If you prefer to follow the iOS design guidelines, you can use the `CupertinoNavigationBar` widget, which is part of the `CupertinoApp`. This will provide an iOS-style navigation bar. Similar to the `AppBar`, you can include it as the `navigationBar` property within the `CupertinoPageScaffold`.

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('My App'),
      ),
      // Other content of your app
    ),
  ));
}
```

The code snippet above demonstrates the usage of `CupertinoNavigationBar` within a `CupertinoApp`. It sets the title of the navigation bar as "My App". Just like the `AppBar`, you can customize properties such as background color, actions, and leading widgets.

## Choosing between the two

Deciding whether to use `AppBar` in `MaterialApp` or `CupertinoNavigationBar` in `CupertinoApp` depends on the design language you want to follow. If you want your app to have a Material Design look and feel, go with `AppBar`. On the other hand, if you prefer an iOS-style interface, choose `CupertinoNavigationBar`.

Remember to import the necessary packages (`material.dart` for `AppBar` and `cupertino.dart` for `CupertinoNavigationBar`) in your code to use these widgets.

For more information, refer to the official Flutter documentation:
- [AppBar class](https://api.flutter.dev/flutter/material/AppBar-class.html)
- [CupertinoNavigationBar class](https://api.flutter.dev/flutter/cupertino/CupertinoNavigationBar-class.html)

#flutter #appbar
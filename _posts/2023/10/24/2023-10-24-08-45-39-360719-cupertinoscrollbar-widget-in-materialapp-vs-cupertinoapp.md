---
layout: post
title: "CupertinoScrollbar widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When working with Flutter, you have the option to choose between two different app frameworks: `MaterialApp` and `CupertinoApp`. While `MaterialApp` is designed to follow the Material Design guidelines, `CupertinoApp` follows the iOS design guidelines.

One of the main differences between these two frameworks is the availability of widgets specific to each design language. In the case of scrollbars, Flutter provides both `Scrollbar` and `CupertinoScrollbar` widgets. 

The `Scrollbar` widget is included in the `material.dart` package and is primarily used when developing apps with `MaterialApp`. It provides a Material Design scrollbar that can be customized to match the app theme using properties such as `thickness` and `radius`. 

On the other hand, the `CupertinoScrollbar` widget is included in the `cupertino.dart` package and is used when developing apps with `CupertinoApp`. It provides an iOS-style scrollbar that blends seamlessly with the Cupertino design language.

## Usage

To use the `Scrollbar` widget in a `MaterialApp`, you can wrap it around a scrollable widget such as `ListView`, `GridView`, or `SingleChildScrollView`. Here's an example of how to use it:

```dart
Scrollbar(
  child: ListView(
    children: [
      // list items
    ],
  ),
)
```

To use the `CupertinoScrollbar`, you can follow the same approach as above, but wrap it around a widget provided by `Cupertino` package, such as `CupertinoListView` or `CustomScrollView`. Here's an example:

```dart
CupertinoScrollbar(
  child: CustomScrollView(
    slivers: [
      // sliver list items
    ],
  ),
)
```

By using the appropriate scrollbar widget based on your chosen app framework, you can ensure that your app's scrolling experience aligns with the design language you are targeting.

It's worth noting that if you use `CupertinoScrollbar` within a `MaterialApp` or vice versa, the scrollbar will still function properly, but its appearance may not match the intended design language.

Make sure to import the required packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';
```

In conclusion, the `CupertinoScrollbar` widget is intended for use with `CupertinoApp`, while the `Scrollbar` widget is designed for `MaterialApp`. Using the appropriate scrollbar widget will help you maintain a consistent and harmonious user interface in your Flutter apps.

## References
- [Flutter documentation on Scrollbar](https://api.flutter.dev/flutter/material/Scrollbar-class.html)
- [Flutter documentation on CupertinoScrollbar](https://api.flutter.dev/flutter/cupertino/CupertinoScrollbar-class.html) 
- [Flutter documentation on MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [Flutter documentation on CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
- [Material Design Guidelines](https://material.io)
- [Cupertino Design Guidelines](https://developer.apple.com/design/human-interface-guidelines)
---
layout: post
title: "Grid view widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In this blog post, we will compare the `GridView` widget in `MaterialApp` and `CupertinoApp`, two popular frameworks for building cross-platform mobile applications.

## Introduction

`MaterialApp` and `CupertinoApp` are both frameworks provided by Flutter for developing mobile applications. While `MaterialApp` follows the material design guidelines and provides a set of widgets that have a material look and feel, `CupertinoApp` follows the design language of iOS and provides widgets that resemble the Cupertino style found in iOS applications.

## Grid View Widget

The `GridView` widget is commonly used for displaying a collection of items in a grid layout. It is versatile and can adapt to different screen sizes and orientations. Let's explore how the `GridView` widget is used within `MaterialApp` and `CupertinoApp`.

### MaterialApp

To use the `GridView` widget within a `MaterialApp`, you can simply wrap it inside a `Scaffold` widget. Here is an example code snippet to illustrate this:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
     home: Scaffold(
       appBar: AppBar(
         title: Text('Grid View Example'),
       ),
       body: GridView.count(
         crossAxisCount: 2,
         children: List.generate(10, (index) {
           return Center(
             child: Text('Item $index'),
           );
         }),
       ),
     ),
  ));
}
```

In this example, we define a `Scaffold` as the home widget in the `MaterialApp`. Within the `body` property of the `Scaffold`, we use the `GridView.count` constructor to create a grid with a specified number of columns. We pass a `crossAxisCount` value of `2`, indicating that we want the grid to have two columns. We then use the `List.generate` method to dynamically generate a list of items inside the grid.

### CupertinoApp

Similarly, we can use the `GridView` widget in a `CupertinoApp`, but the surrounding widgets will differ. Here is an example code snippet to illustrate this:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Grid View Example'),
      ),
      child: SafeArea(
        child: GridView.count(
          crossAxisCount: 2,
          children: List.generate(10, (index) {
            return Center(
              child: Text('Item $index'),
            );
          }),
        ),
      ),
    ),
  ));
}
```

In this example, we use the `CupertinoPageScaffold` widget as the `home` widget of the `CupertinoApp`. Inside the `CupertinoPageScaffold`, we include a `CupertinoNavigationBar` to define the navigation bar at the top of the screen. The grid itself is wrapped in a `SafeArea` widget to ensure it respects the safe area boundaries of the device.

## Conclusion

In this blog post, we compared the usage of the `GridView` widget within the `MaterialApp` and `CupertinoApp` frameworks. While the code structure may differ slightly between the two, the `GridView` widget itself remains consistent and allows you to create versatile grid layouts in both material and Cupertino styles. Feel free to explore further possibilities and customization options with the `GridView` widget in Flutter.

**References:**
- Flutter Documentation: [GridView](https://api.flutter.dev/flutter/widgets/GridView-class.html)
- Flutter Documentation: [MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- Flutter Documentation: [CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
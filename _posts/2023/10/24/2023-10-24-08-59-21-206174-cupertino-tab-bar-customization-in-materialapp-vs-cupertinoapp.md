---
layout: post
title: "Cupertino tab bar customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When building a Flutter app, you have the option to use either `MaterialApp` or `CupertinoApp` widgets as the base for your app's theme and layout. These widgets come with their own set of UI components, including the tab bar. In this blog post, we will explore how to customize the Cupertino tab bar in both `MaterialApp` and `CupertinoApp` to create a cohesive and visually appealing app.

## Customizing the tab bar in MaterialApp

Flutter's `MaterialApp` widget is based on the Material Design principles. If you opt to use `MaterialApp`, you get access to the `Material` library that provides various customizable UI components. To customize the tab bar in `MaterialApp`, you can follow these steps:

1. Import the necessary libraries:
```dart
import 'package:flutter/material.dart';
```

2. Create a `TabBar` widget and define its properties:
```dart
TabBar(
  tabs: [
    Tab(text: 'Tab 1'),
    Tab(text: 'Tab 2'),
    Tab(text: 'Tab 3'),
  ],
  indicatorColor: Colors.blue, // Customize the indicator color
  labelColor: Colors.blue, // Customize the label color
)
```

3. Wrap the `TabBar` widget inside a `DefaultTabController` and a `Scaffold`:
```dart
DefaultTabController(
  length: 3, // Customize the number of tabs
  child: Scaffold(
    appBar: AppBar(
      title: Text('My App'),
      bottom: TabBar(
        tabs: [
          // TabBar definition from step 2
        ],
      ),
    ),
    body: TabBarView(
      children: [
        // Define the content for each tab
      ],
    ),
  ),
)
```

By customizing the `indicatorColor` and `labelColor` properties, you can modify the appearance of the tab bar to suit your app's design requirements.

## Customizing the tab bar in CupertinoApp

If you prefer to follow the iOS design guidelines, you can use the `CupertinoApp` widget, which is based on the Cupertino (iOS) Design System. To customize the tab bar in `CupertinoApp`, follow these steps:

1. Import the necessary libraries:
```dart
import 'package:flutter/cupertino.dart';
```

2. Create a `CupertinoTabBar` widget and define its properties:
```dart
CupertinoTabBar(
  items: [
    BottomNavigationBarItem(icon: Icon(Icons.home)),
    BottomNavigationBarItem(icon: Icon(Icons.search)),
    BottomNavigationBarItem(icon: Icon(Icons.settings)),
  ],
  backgroundColor: CupertinoColors.systemGrey, // Customize the background color
  activeColor: CupertinoColors.activeBlue, // Customize the active tab color
)
```

3. Wrap the `CupertinoTabBar` widget inside a `CupertinoTabScaffold`:
```dart
CupertinoTabScaffold(
  tabBar: CupertinoTabBar(
    items: [
      // TabBar definition from step 2
    ],
  ),
  tabBuilder: (context, index) {
    // Define the content for each tab
  },
)
```

By modifying the `backgroundColor` and `activeColor` properties, you can customize the appearance of the tab bar in your Cupertino-styled app.

## Conclusion

Whether you choose to use the `MaterialApp` or `CupertinoApp` widget for your Flutter app, customizing the tab bar is straightforward. By following the steps outlined above, you can ensure that the tab bar in your app aligns with your design preferences, creating a visually appealing and cohesive user experience.

For more information, refer to the official Flutter documentation on [MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html) and [CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html). 

Stay tuned for more Flutter-related posts! #Flutter #UI
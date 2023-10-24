---
layout: post
title: "Cupertino bottom navigation bar customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [cupertino]
comments: true
share: true
---

In Flutter, you can create a beautiful and customisable bottom navigation bar using the Cupertino design language. There are two different ways to implement this: using the `MaterialApp` widget or the `CupertinoApp` widget. In this blog post, we will explore the differences between the two approaches and see how to customize the Cupertino bottom navigation bar in each case.

## Table of Contents
- [Using MaterialApp](#using-materialapp)
- [Using CupertinoApp](#using-cupertinoapp)
- [Customizing the Cupertino Bottom Navigation Bar](#customizing-the-cupertino-bottom-navigation-bar)
- [Conclusion](#conclusion)

## Using MaterialApp
To use the Cupertino bottom navigation bar in MaterialApp, you need to import the `cupertino_icons` package and wrap your MaterialApp widget inside a Scaffold. Here's an example code snippet:

\```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';
import 'package:flutter/cupertino_icons.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      bottomNavigationBar: CupertinoTabBar(
        items: [
          BottomNavigationBarItem(icon: Icon(CupertinoIcons.home)),
          BottomNavigationBarItem(icon: Icon(CupertinoIcons.search)),
          BottomNavigationBarItem(icon: Icon(CupertinoIcons.settings)),
        ],
      ),
    ),
  ));
}
\```

In the code above, we imported the `cupertino_icons` package and used the `CupertinoTabBar` widget as the `bottomNavigationBar` of our Scaffold. We also provided three `BottomNavigationBarItem` widgets, each with an icon from the `CupertinoIcons` class.

## Using CupertinoApp
If you prefer to use CupertinoApp to set up your Flutter app, the process is slightly different. Instead of wrapping your MaterialApp widget inside a Scaffold, you can directly use the CupertinoTabScaffold widget. Here's an example:

\```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';
import 'package:flutter/cupertino_icons.dart';

void main() {
  runApp(CupertinoApp(
    home: CupertinoTabScaffold(
      tabBar: CupertinoTabBar(
        items: [
          BottomNavigationBarItem(icon: Icon(CupertinoIcons.home)),
          BottomNavigationBarItem(icon: Icon(CupertinoIcons.search)),
          BottomNavigationBarItem(icon: Icon(CupertinoIcons.settings)),
        ],
      ),
      tabBuilder: (context, index) {
        return CupertinoTabView(builder: (context) {
          switch (index) {
            case 0:
              return HomeScreen();
            case 1:
              return SearchScreen();
            case 2:
              return SettingsScreen();
            default:
              return HomeScreen();
          }
        });
      },
    ),
  ));
}
\```

In this code snippet, we used the `CupertinoTabScaffold` widget and provided a tabBuilder function to handle the content of each tab. We created separate screen widgets for each tab (HomeScreen, SearchScreen, SettingsScreen) and returned the appropriate screen based on the selected index.

## Customizing the Cupertino Bottom Navigation Bar
To customize the appearance of the Cupertino bottom navigation bar, you can change various properties of the `CupertinoTabBar` widget. Here are some examples:

- `backgroundColor`: Sets the background color of the navigation bar.
- `activeColor`: Sets the color of the selected item.
- `inactiveColor`: Sets the color of the unselected items.
- `iconSize`: Sets the size of the icons.
- `border`: Sets a border for the navigation bar.

You can also customize individual icons in the bottom navigation bar by using the `icon` property of the `BottomNavigationBarItem` widget.

## Conclusion
In this blog post, we discussed how to implement a custom Cupertino bottom navigation bar using either MaterialApp or CupertinoApp. We explored the differences between the two approaches and saw how to customize the appearance of the navigation bar in each case. Whether you choose to use MaterialApp or CupertinoApp, Flutter provides the flexibility to create a beautiful and customisable navigation experience for your app.

#flutter #cupertino
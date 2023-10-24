---
layout: post
title: "CupertinoTabScaffold widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing a Flutter application, you may come across the choice between using the `CupertinoTabScaffold` widget within the `MaterialApp` widget or using the `CupertinoApp` widget for a Cupertino-style navigation experience. In this blog post, we will compare the two approaches and help you decide which one suits your needs better.

## Understanding the Widgets
Before diving into the comparison, let's understand what each of these widgets does:

### MaterialApp
`MaterialApp` is the main widget used in Flutter to build applications with Material Design. It provides a Material-style layout and navigation system, including features like an app bar, drawer, and bottom navigation bar. It is ideal for creating applications that follow the Material Design guidelines.

### CupertinoApp
`CupertinoApp` is a widget used to create applications with an iOS-like user interface. It provides a Cupertino-style layout and navigation system, featuring navigation bars, tab bars, and more. It is perfect for creating applications with a native iOS look and feel.

### CupertinoTabScaffold
`CupertinoTabScaffold` is a widget used to create a tab-based navigation layout. It provides a container for multiple screens (or tabs), along with a bottom navigation bar that allows the user to switch between them.

## Using CupertinoTabScaffold with MaterialApp
One approach is to use the `CupertinoTabScaffold` widget within the `MaterialApp` widget. This allows you to combine the Material Design elements provided by `MaterialApp` with the tab-based navigation layout of `CupertinoTabScaffold`. This approach is suitable if you want to have a mixed design, with Material Design components and iOS-style tab navigation in your app.

To use `CupertinoTabScaffold` with `MaterialApp`, you need to import the `cupertino.dart` file and wrap your `MaterialApp` widget with a `CupertinoTabScaffold` widget. Inside the `CupertinoTabScaffold`, you can define your tabs using `CupertinoTabBar` and `CupertinoTabView` widgets.

Here's an example:

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CupertinoTabScaffold(
        tabBar: CupertinoTabBar(
          items: [
            BottomNavigationBarItem(
              icon: Icon(Icons.home),
              label: 'Home',
            ),
            BottomNavigationBarItem(
              icon: Icon(Icons.settings),
              label: 'Settings',
            ),
          ],
        ),
        tabBuilder: (context, index) {
          return CupertinoTabView(
            builder: (context) {
              return Container(
                child: Center(
                  child: Text('Tab $index'),
                ),
              );
            },
          );
        },
      ),
    );
  }
}
```

## Using CupertinoApp for Full Cupertino Experience
Another approach is to use the `CupertinoApp` widget as the root widget of your application. With `CupertinoApp`, you get a complete Cupertino-style app experience, including iOS-style theming and navigation.

To use `CupertinoApp`, simply create an instance of it as your root widget and define your tabs using the `CupertinoTabBar` and `CupertinoTabView` widgets as before.

Here's an example:

```dart
import 'package:flutter/cupertino.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      home: CupertinoTabScaffold(
        tabBar: CupertinoTabBar(
          items: [
            BottomNavigationBarItem(
              icon: Icon(Icons.home),
              label: 'Home',
            ),
            BottomNavigationBarItem(
              icon: Icon(Icons.settings),
              label: 'Settings',
            ),
          ],
        ),
        tabBuilder: (context, index) {
          return CupertinoTabView(
            builder: (context) {
              return Container(
                child: Center(
                  child: Text('Tab $index'),
                ),
              );
            },
          );
        },
      ),
    );
  }
}
```

## Conclusion
In conclusion, if you want to mix Material Design elements with a tab-based navigation layout, you can use the `CupertinoTabScaffold` widget within the `MaterialApp` widget. However, if you desire a full Cupertino experience with iOS-style theming and navigation, the `CupertinoApp` widget is the way to go.

Choose the approach that best fits the design and functionality requirements of your application and enjoy developing beautiful Flutter apps.

#flutter #ios
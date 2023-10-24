---
layout: post
title: "Tab bar widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

Tab bars are a common user interface component in mobile applications. They allow users to switch between different sections or views of an app with just a single tap. In Flutter, there are two main ways to implement tab bars: using the `TabBar` widget in a `MaterialApp` or using the `CupertinoTabBar` widget in a `CupertinoApp`. 

## Tab Bar in MaterialApp

The `TabBar` widget is part of the Material package and provides a tab bar functionality that follows the Material Design guidelines. To use the `TabBar` widget, you need to wrap your app's `Scaffold` widget with a `DefaultTabController` widget. This allows the `TabBar` to track the selected tab and update the content accordingly. 

Here's an example of how to use the `TabBar` widget in a `MaterialApp`:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: DefaultTabController(
      length: 2, // number of tabs
      child: Scaffold(
        appBar: AppBar(
          title: Text('Tab Bar Example'),
          bottom: TabBar(
            tabs: [
              Tab(icon: Icon(Icons.home), text: 'Home'),
              Tab(icon: Icon(Icons.settings), text: 'Settings'),
            ],
          ),
        ),
        body: TabBarView(
          children: [
            HomeTab(),
            SettingsTab(),
          ],
        ),
      ),
    ),
  ));
}

class HomeTab extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Text('Home Tab Content'),
    );
  }
}

class SettingsTab extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Text('Settings Tab Content'),
    );
  }
}
```

## Tab Bar in CupertinoApp

If you want to follow the design guidelines of iOS, you can use the `CupertinoTabBar` widget in a `CupertinoApp`. The `CupertinoTabBar` provides a tab bar that mimics the look and behavior of the iOS tab bar. Similarly to the `TabBar` widget, you'll need to wrap your app's `CupertinoTabScaffold` widget with a `CupertinoTabController` to handle the selected tab.

Here's an example of how to use the `CupertinoTabBar` widget in a `CupertinoApp`:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: CupertinoTabScaffold(
      tabBar: CupertinoTabBar(
        items: [
          BottomNavigationBarItem(icon: Icon(CupertinoIcons.home), label: 'Home'),
          BottomNavigationBarItem(icon: Icon(CupertinoIcons.settings), label: 'Settings'),
        ],
      ),
      tabBuilder: (BuildContext context, int index) {
        if (index == 0) {
          return CupertinoTabView(
            builder: (BuildContext context) {
              return CupertinoPageScaffold(
                navigationBar: CupertinoNavigationBar(
                  middle: Text('Home'),
                ),
                child: Center(
                  child: Text('Home Tab Content'),
                ),
              );
            },
          );
        } else {
          return CupertinoTabView(
            builder: (BuildContext context) {
              return CupertinoPageScaffold(
                navigationBar: CupertinoNavigationBar(
                  middle: Text('Settings'),
                ),
                child: Center(
                  child: Text('Settings Tab Content'),
                ),
              );
            },
          );
        }
      },
    ),
  ));
}
```

As you can see, using the `CupertinoTabBar` in a `CupertinoApp` requires a slightly different setup compared to the `TabBar` in a `MaterialApp`. However, both approaches offer a convenient way to implement tab bars in your Flutter applications, depending on the desired design style.

## Conclusion

In summary, if you want a tab bar that follows the Material Design guidelines, you can use the `TabBar` widget in a `MaterialApp`. On the other hand, if you want to adhere to the iOS design guidelines, you can opt for the `CupertinoTabBar` widget in a `CupertinoApp`. Both widgets provide a straightforward way to implement tab bar functionality in your Flutter apps.
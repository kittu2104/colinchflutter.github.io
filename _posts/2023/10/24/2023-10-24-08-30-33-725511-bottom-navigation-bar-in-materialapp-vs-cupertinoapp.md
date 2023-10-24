---
layout: post
title: "Bottom navigation bar in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing a mobile application, one crucial aspect is the navigation system. Two popular choices for building a bottom navigation bar in mobile apps are using `MaterialApp` in Flutter with Google's Material Design or using `CupertinoApp` in Flutter with Apple's Cupertino design.

## Overview

The `MaterialApp` widget provides a comprehensive set of widgets following Google's Material Design guidelines. On the other hand, the `CupertinoApp` widget implements Apple's iOS design guidelines with the Cupertino look and feel.

Both `MaterialApp` and `CupertinoApp` offer a bottom navigation bar to allow users to navigate between different screens or sections of the app. However, there are some differences in their appearance and behavior.

## Material Design Bottom Navigation Bar (MaterialApp)

To create a bottom navigation bar using Google's Material Design, you can utilize the `BottomNavigationBar` widget provided by the `MaterialApp`. Here's an example code snippet:

```dart
MaterialApp(
  home: Scaffold(
    bottomNavigationBar: BottomNavigationBar(
      items: [
        BottomNavigationBarItem(
          icon: Icon(Icons.home),
          label: 'Home',
        ),
        BottomNavigationBarItem(
          icon: Icon(Icons.search),
          label: 'Search',
        ),
        BottomNavigationBarItem(
          icon: Icon(Icons.settings),
          label: 'Settings',
        ),
      ],
    ),
  ),
)
```

The `BottomNavigationBar` widget accepts a list of `BottomNavigationBarItem` widgets that define each item in the navigation bar. Each `BottomNavigationBarItem` consists of an `icon` and a `label`.

## Cupertino Design Bottom Navigation Bar (CupertinoApp)

To create a bottom navigation bar resembling Apple's iOS design, you can use the `CupertinoTabBar` widget provided by the `CupertinoApp`. Here's an example code snippet:

```dart
CupertinoApp(
  home: CupertinoTabScaffold(
    tabBar: CupertinoTabBar(
      items: [
        BottomNavigationBarItem(
          icon: Icon(Icons.home),
          label: 'Home',
        ),
        BottomNavigationBarItem(
          icon: Icon(Icons.search),
          label: 'Search',
        ),
        BottomNavigationBarItem(
          icon: Icon(Icons.settings),
          label: 'Settings',
        ),
      ],
    ),
    tabBuilder: (context, index) {
      // Return the appropriate screen based on the selected index.
    },
  ),
)
```

In this code snippet, the `CupertinoTabBar` widget is used within `CupertinoTabScaffold`. Similar to `BottomNavigationBar`, `CupertinoTabBar` requires a list of `BottomNavigationBarItem` widgets to define the items in the navigation bar.

## Conclusion

Both `MaterialApp` and `CupertinoApp` offer bottom navigation bars with different designs and behaviors. The choice between them depends on the specific design guidelines you wish to follow for your mobile app. By utilizing the appropriate widgets and following the respective design guidelines, you can create a visually cohesive and user-friendly navigation experience for your users.

**References:**
- [BottomNavigationBar class - Flutter API Documentation](https://api.flutter.dev/flutter/material/BottomNavigationBar-class.html)
- [CupertinoTabBar class - Flutter API Documentation](https://api.flutter.dev/flutter/cupertino/CupertinoTabBar-class.html)
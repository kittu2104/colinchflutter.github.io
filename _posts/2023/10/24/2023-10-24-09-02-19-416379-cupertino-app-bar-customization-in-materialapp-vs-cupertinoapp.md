---
layout: post
title: "Cupertino app bar customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing mobile applications using Flutter, you have the option to choose between two main design systems: Material Design and Cupertino. Material Design follows the guidelines set by Google, while Cupertino mimics the iOS design patterns.

One of the key components in any mobile app is the app bar, which typically contains the title, navigation icons, and other relevant actions. In Flutter, you have two options for customizing the app bar based on the design system you choose: MaterialApp and CupertinoApp.

Let's delve into the customization options for the app bar in each scenario.

## MaterialApp App Bar Customization
If you're using MaterialApp, which is the default design system for Flutter, you have access to the `AppBar` widget. This widget allows you to easily customize the app bar's appearance and behavior.

### Basic App Bar
To create a basic app bar, you can use the `AppBar` widget and provide it with a `title` parameter to set the title of the app bar:

```dart
import 'package:flutter/material.dart';

AppBar(
  title: Text('App Bar Title'),
)
```

### Adding Actions
You can also add actions to the app bar, such as icons for navigation or additional functionalities. To do this, you can utilize the `actions` parameter of the `AppBar` widget and provide a list of `IconButton` widgets:

```dart
AppBar(
  title: Text('App Bar Title'),
  actions: [
    IconButton(
      icon: Icon(Icons.search),
      onPressed: () {
        // Perform search action
      },
    ),
    IconButton(
      icon: Icon(Icons.settings),
      onPressed: () {
        // Open settings screen
      },
    ),
  ],
)
```

By adding more `IconButton` widgets to the `actions` list, you can easily expand the functionality of the app bar.

## CupertinoApp App Bar Customization
If you choose to use the Cupertino design system, you can customize the app bar using the `CupertinoNavigationBar` widget.

### Basic App Bar
To create a basic app bar in Cupertino, you can use the `CupertinoNavigationBar` widget and provide it with a `middle` parameter to set the title of the app bar:

```dart
import 'package:flutter/cupertino.dart';

CupertinoNavigationBar(
  middle: Text('App Bar Title'),
)
```

### Adding Actions
Similar to the `AppBar` widget, you can add actions to the Cupertino app bar using the `trailing` parameter. You can provide a list of widgets as the `trailing` parameter:

```dart
CupertinoNavigationBar(
  middle: Text('App Bar Title'),
  trailing: Row(
    mainAxisSize: MainAxisSize.min,
    children: [
      CupertinoButton(
        padding: EdgeInsets.zero,
        child: Icon(
          CupertinoIcons.search,
          size: 28,
        ),
        onPressed: () {
          // Perform search action
        },
      ),
      CupertinoButton(
        padding: EdgeInsets.zero,
        child: Icon(
          CupertinoIcons.settings,
          size: 28,
        ),
        onPressed: () {
          // Open settings screen
        },
      ),
    ],
  ),
)
```

By customizing the `trailing` property, you can add multiple actions or icons to the Cupertino app bar.

## Conclusion
When it comes to customizing the app bar in Flutter, you have the flexibility to choose between MaterialApp and CupertinoApp based on your design preferences. Whether you opt for the Material Design system provided by MaterialApp or the iOS-inspired design of CupertinoApp, both offer easy ways to customize and enhance the app bar.

Remember to consider your target audience and design guidelines when choosing the appropriate app bar customization method for your Flutter app.

**References:**
- [Material Design](https://material.io/design)
- [Cupertino iOS Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/ios/overview/themes/#:~:text=The%20human%20interface%20guidelines%20provide,and%20fonts%20to%20your%20app.)
---
layout: post
title: "MediaQuery accessibleNavigationChanged in Flutter"
description: " "
date: 2023-10-01
tags: [Flutter, Accessibility]
comments: true
share: true
---

When building accessible user interfaces in Flutter, you often need to adapt your app's behavior based on the user's accessibility settings. Flutter provides the `MediaQuery` class to help you retrieve information about the user's device and system settings. One important aspect of accessibility is navigation, and Flutter provides the `accessibleNavigationChanged` property of `MediaQuery` to detect changes in the user's navigation method.

## What is accessibleNavigationChanged?

The `accessibleNavigationChanged` property is a boolean value that indicates whether the user's accessible navigation mode has changed. This property is part of the `MediaQueryData` object that you can retrieve using `MediaQuery.of(context)`.

Accessible navigation modes include options like "direct selection" or "single switch scanning" that assist users with limited mobility or disabilities in navigating through user interfaces. By detecting changes in this mode, you can adapt your app's behavior to provide a better user experience for individuals with accessibility needs.

## Example Usage

Here's an example on how to use the `accessibleNavigationChanged` property in your Flutter app:

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  bool _accessibleNavigationChanged = false;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Accessible Navigation'),
      ),
      body: Builder(
        builder: (context) {
          final MediaQueryData mediaQuery = MediaQuery.of(context);
          final bool accessibleNavigationChanged = mediaQuery.accessibleNavigationChanged;

          if (accessibleNavigationChanged != _accessibleNavigationChanged) {
            setState(() {
              _accessibleNavigationChanged = accessibleNavigationChanged;
            });

            // Add your logic to handle accessible navigation mode changes
          }

          return Center(
            child: Text(
              accessibleNavigationChanged ? 'Accessible Navigation On' : 'Accessible Navigation Off',
              style: TextStyle(fontSize: 24),
            ),
          );
        },
      ),
    );
  }
}
```

In this example, we create a `MyWidget` class that extends `StatefulWidget`. Inside its state, we declare a boolean variable `_accessibleNavigationChanged` to track changes in the accessible navigation mode. In the `build` method, we use a `Builder` widget to access the `MediaQuery` and retrieve the `accessibleNavigationChanged` property. If the value has changed, we update the state and perform any necessary actions based on the new mode.

Finally, we display a simple `Text` widget that shows whether the accessible navigation mode is turned on or off.

## Conclusion

The `accessibleNavigationChanged` property provided by `MediaQuery` in Flutter allows you to detect changes in the user's accessible navigation mode. By leveraging this property, you can create more inclusive and accessible user interfaces that adapt to the needs of all users.

#Flutter #Accessibility
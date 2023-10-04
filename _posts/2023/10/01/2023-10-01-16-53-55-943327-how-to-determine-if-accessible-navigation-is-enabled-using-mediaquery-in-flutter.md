---
layout: post
title: "How to determine if accessible navigation is enabled using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [accessibility]
comments: true
share: true
---

In Flutter, you can determine if accessible navigation is enabled by using `MediaQuery`. `MediaQuery` is a class that provides information about the current device's size, orientation, and accessibility settings.

To check if accessible navigation is enabled, you can use the `accessibleNavigation` property of `MediaQueryData`. This property returns a boolean value indicating whether the accessible navigation feature is enabled or not.

Here's an example code snippet that demonstrates how to determine if accessible navigation is enabled using `MediaQuery` in Flutter:

```dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final MediaQueryData mediaQueryData = MediaQuery.of(context);
    final bool isAccessibleNavigationEnabled =
        mediaQueryData.accessibleNavigation;

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Accessible Navigation'),
        ),
        body: Center(
          child: Text(
            'Accessible Navigation Enabled: $isAccessibleNavigationEnabled',
            style: TextStyle(fontSize: 20),
          ),
        ),
      ),
    );
  }
}

void main() {
  runApp(MyApp());
}
```

In this example, we obtain the `MediaQueryData` using `MediaQuery.of(context)`. Then, we extract the `accessibleNavigation` property to check if accessible navigation is enabled or not. Finally, we display the result on the screen using a `Text` widget.

Remember to wrap your `Text` widget with `Center` or any other appropriate widget to properly align it on the screen.

When running the above code, if accessible navigation is enabled on the device, it will display "Accessible Navigation Enabled: true". Otherwise, it will display "Accessible Navigation Enabled: false".

By using this technique, you can dynamically adjust the user interface or behavior of your Flutter app based on the accessibility settings of the device.

#flutter #accessibility
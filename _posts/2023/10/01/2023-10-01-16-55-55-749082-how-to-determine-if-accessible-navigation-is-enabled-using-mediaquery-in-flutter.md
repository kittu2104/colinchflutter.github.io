---
layout: post
title: "How to determine if accessible navigation is enabled using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [Accessibility]
comments: true
share: true
---

In Flutter, you can determine if accessible navigation is enabled by using `MediaQueryData` class and its `accessibleNavigation` property. The `accessibleNavigation` property is a boolean value that indicates whether the device has accessibility features enabled for navigation.

To check if accessible navigation is enabled, follow these steps:

1. Get the `MediaQueryData` instance by using `MediaQuery.of(context)`.

2. Access the `accessibleNavigation` property of the `MediaQueryData` instance. This will give you a boolean value indicating whether accessible navigation is enabled.

Here's an example code snippet that demonstrates how to determine if accessible navigation is enabled:

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Get the MediaQueryData instance
    final mediaQueryData = MediaQuery.of(context);

    // Check if accessible navigation is enabled
    final isAccessibleNavigationEnabled = mediaQueryData.accessibleNavigation;

    // Use the boolean value
    if (isAccessibleNavigationEnabled) {
      // Accessible navigation is enabled
      // Add your code here
    } else {
      // Accessible navigation is disabled
      // Add your code here
    }

    // Add your remaining widget code here
    return Container();
  }
}
```

In the example above, the `isAccessibleNavigationEnabled` variable is used to check whether accessible navigation is enabled or disabled. You can use this boolean value to conditionally render different UI elements or apply specific logic based on the accessibility settings of the device.

Hashtags: #Flutter #Accessibility
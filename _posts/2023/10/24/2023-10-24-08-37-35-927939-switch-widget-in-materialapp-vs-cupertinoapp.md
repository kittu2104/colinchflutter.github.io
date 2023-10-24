---
layout: post
title: "Switch widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

In Flutter, there are two main ways to create a switch widget: using the `Switch` widget within a `MaterialApp` or using the `CupertinoSwitch` widget within a `CupertinoApp`. Each approach offers a different visual style that aligns with the design language of the platform.

Let's explore the differences between the two options:

## `Switch` in `MaterialApp`

When using the `Switch` widget within a `MaterialApp`, you will get a switch that reflects the material design guidelines. It has a flat rectangular shape and a thumb that animates when the user taps on it. Here's an example of how to use the `Switch` widget in a `MaterialApp`:

```dart
import 'package:flutter/material.dart';

// ...

Switch(
  value: true,
  onChanged: (bool value) {
    // Handle the switch state change
    setState(() {
      // Update the switch state here
    });
  },
)
```

## `CupertinoSwitch` in `CupertinoApp`

On the other hand, when using the `CupertinoSwitch` widget within a `CupertinoApp`, you will get a switch that follows the visual style of iOS. It has a circular shape with a sliding animation when the user interacts with it. Here's an example of how to use the `CupertinoSwitch` widget in a `CupertinoApp`:

```dart
import 'package:flutter/cupertino.dart';

// ...

CupertinoSwitch(
  value: true,
  onChanged: (bool value) {
    // Handle the switch state change
    setState(() {
      // Update the switch state here
    });
  },
)
```

## Choosing Between `Switch` and `CupertinoSwitch`

The choice between these two switch widgets mainly depends on the overall design language of your app and the target platform. If you are building an app that follows the material design guidelines and targets Android and other platforms, using the `Switch` widget within the `MaterialApp` is usually the best choice.

On the other hand, if you are building an app that specifically targets iOS and wants to achieve an iOS-like look and feel, using the `CupertinoSwitch` widget within the `CupertinoApp` is the way to go.

By choosing the appropriate switch widget, you can ensure that your app's UI elements align with the platform's design language, providing a more cohesive and familiar user experience.

**References:**
- `Switch` class: [https://api.flutter.dev/flutter/material/Switch-class.html](https://api.flutter.dev/flutter/material/Switch-class.html)
- `CupertinoSwitch` class: [https://api.flutter.dev/flutter/cupertino/CupertinoSwitch-class.html](https://api.flutter.dev/flutter/cupertino/CupertinoSwitch-class.html)

**#flutter #ui**
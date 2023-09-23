---
layout: post
title: "Handling different screen resolutions with `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [Flutter, MobileAppDevelopment]
comments: true
share: true
---

First, let's import the necessary packages:

```dart
import 'package:flutter/material.dart';
```

Next, we can use the `MediaQuery` class to retrieve the device's screen size and other attributes within a widget. Here's an example of a `Container` widget that adapts its width based on the screen width:

```dart
Container(
  width: MediaQuery.of(context).size.width * 0.8,
  height: 200,
  color: Colors.blue,
)
```

In the above snippet, we access the screen width by calling `MediaQuery.of(context).size.width`. We then multiply it by `0.8` to set the `Container` width to 80% of the screen width.

You can also leverage `MediaQuery` to make adjustments based on different screen densities. For example, if you want to display different images for different screen densities, you can use the `devicePixelRatio` property:

```dart
if (MediaQuery.of(context).devicePixelRatio > 2.0) {
  // Load high-resolution image
} else {
  // Load regular-resolution image
}
```

In this code, we check if the `devicePixelRatio` is greater than `2.0`, indicating a high-resolution device. Depending on the result, you can load a high-resolution image or a regular-resolution image accordingly.

By using `MediaQuery` in Flutter, you can dynamically adapt your UI elements to fit various screen sizes and pixel densities. This ensures that your app looks great on devices with different resolutions, enhancing the user experience.

Remember to import the `material.dart` package to access `MediaQuery` class.

#Flutter #MobileAppDevelopment
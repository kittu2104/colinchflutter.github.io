---
layout: post
title: "How to retrieve the device's text style using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [flutterdevelopment]
comments: true
share: true
---

When developing a Flutter application, it's important to ensure that the text style used in your app is consistent across various devices. One way to achieve this is by retrieving the device's text style using `MediaQuery`.

## What is MediaQuery?

`MediaQuery` is a Flutter widget that provides information about the device's size, orientation, and pixel density. It is commonly used to build responsive layouts that adapt to different screen sizes.

## Retrieving the Text Style

To retrieve the device's text style, you can use the `MediaQuery` class in combination with the `textScaleFactor` property. The `textScaleFactor` property returns the current text scale factor set on the device.

Here's an example of how you can retrieve the device's text style using `MediaQuery` in Flutter:

```dart
import 'package:flutter/material.dart';

class YourWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final textScaleFactor = MediaQuery.of(context).textScaleFactor;

    // Use the textScaleFactor to adjust the text style
    final textStyle = TextStyle(
      fontSize: 16 * textScaleFactor,
      fontWeight: FontWeight.normal,
    );

    return Text(
      'Your text',
      style: textStyle,
    );
  }
}
```

In the example above, we first retrieve the `textScaleFactor` using `MediaQuery.of(context).textScaleFactor`. We then use this value to adjust the text style by multiplying the base font size (16) with the `textScaleFactor`.

This ensures that the text size on the device is adjusted based on the user's preference or accessibility settings.

## Conclusion

Retrieving the device's text style using `MediaQuery` in Flutter allows you to build apps with consistent text sizes across different devices. By leveraging `textScaleFactor`, you can ensure a good user experience for all users.

#flutter #flutterdevelopment
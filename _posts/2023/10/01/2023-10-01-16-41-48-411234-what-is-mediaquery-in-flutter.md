---
layout: post
title: "What is MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [MediaQuery]
comments: true
share: true
---

In Flutter, `MediaQuery` is a class that allows developers to obtain information about the current device's screen size, orientation, and other display-related properties. It provides a way to design responsive and adaptive layouts that can adapt to different screen sizes and orientations.

## Importance of MediaQuery

With the wide range of devices in the market, it is crucial for developers to create apps that can adjust their layout and appearance according to the device's screen size and orientation. Creating static layouts that do not adapt to different screen sizes can result in poor user experience and may lead to elements being cut off or displayed incorrectly on smaller or larger screens.

By utilizing `MediaQuery`, developers can dynamically adjust the layout, font sizes, padding, and other UI elements based on the current device's screen properties. This ensures that the app looks consistent and functions properly on various devices.

## Usage of MediaQuery

To use `MediaQuery`, you first need to access it using the `MediaQuery.of(context)` method. This method requires the `BuildContext` as a parameter, which is typically obtained from the `build` method of a widget.

```dart
MediaQueryData mediaQuery = MediaQuery.of(context);
```

Once you have access to the `MediaQueryData`, you can retrieve various properties, such as:

- `mediaQuery.size`: provides the `Size` of the current device's screen.

- `mediaQuery.orientation`: gives the `Orientation` of the device (`Portrait` or `Landscape`).

- `mediaQuery.devicePixelRatio`: provides the device's pixel ratio, which is useful for handling high-density screens.

- `mediaQuery.padding`: gives the padding values that are automatically applied by the operating system to avoid content overlapping with system elements.

These properties can be used to dynamically adjust widget sizes, fonts, paddings, and margins based on the current device's screen properties.

## Example of MediaQuery Usage

```dart
import 'package:flutter/material.dart';

class ResponsiveWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final mediaQuery = MediaQuery.of(context);

    return Container(
      width: mediaQuery.size.width * 0.8, // Adjusts container width to 80% of the device's width
      height: mediaQuery.size.height, // Takes the entire height of the device
      padding: mediaQuery.padding, // Uses automatic padding values given by the system
      child: Text(
        'Hello, Flutter!',
        style: TextStyle(fontSize: mediaQuery.size.width * 0.05), // Adjusts font size based on device width
      ),
    );
  }
}
```

In the above code snippet, we used `MediaQuery` to adjust the width and height of a container based on the device's screen dimensions. We also used the device's padding to set the padding value of the container, and adjusted the font size of the text based on the width of the device.

By utilizing `MediaQuery`, we can create responsive and adaptive UIs that provide a consistent experience across various devices.

#Flutter #MediaQuery
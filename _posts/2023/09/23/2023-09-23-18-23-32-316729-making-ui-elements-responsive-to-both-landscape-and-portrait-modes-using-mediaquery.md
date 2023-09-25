---
layout: post
title: "Making UI elements responsive to both landscape and portrait modes using `MediaQuery`"
description: " "
date: 2023-09-23
tags: [ResponsiveDesign]
comments: true
share: true
---

In today's digital world, it has become crucial for mobile applications to provide a seamless user experience across different device orientations. One way to achieve this is by making UI elements responsive to both landscape and portrait modes. In this blog post, we will explore how to achieve this using the `MediaQuery` class in Flutter.

## What is MediaQuery?

`MediaQuery` is a powerful class in the Flutter framework that allows us to obtain information about the current device's screen size, pixel density, and orientation. It provides a convenient way to make UI elements responsive by adjusting their layout and behavior based on the available screen real estate.

## Detecting Device Orientation

To make UI elements responsive, we first need to determine the current device orientation. We can do this using the `MediaQuery.of` method. Let's take a look at an example:

```dart
import 'package:flutter/material.dart';

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final orientation = MediaQuery.of(context).orientation;
  
    if (orientation == Orientation.landscape) {
      // Render UI for landscape mode
      return Container(
        child: Text('Landscape Mode'),
      );
    } else {
      // Render UI for portrait mode
      return Container(
        child: Text('Portrait Mode'),
      );
    }
  }
}
```

In the above code snippet, we obtain the device orientation using `MediaQuery.of(context).orientation`. We then conditionally render UI elements based on whether the orientation is landscape or portrait.

## Adjusting UI for Different Orientations

Once we have detected the device orientation, we can adjust our UI layout and behavior accordingly. Here are a few techniques to make UI elements responsive:

### 1. Flex Widgets

Flex widgets like `Row` and `Column` are great for adjusting UI elements based on available space. You can set flexible properties like `Expanded` or `Flexible` within these widgets to ensure that UI elements expand or shrink as per the orientation.

### 2. MediaQuery.of(context).size

To calculate the available screen size, you can use `MediaQuery.of(context).size`. This returns a `Size` object with the height and width of the screen. You can adjust the layout, font sizes, or padding values based on the screen size.

### 3. MediaQuery.of(context).devicePixelRatio

The `MediaQuery.of(context).devicePixelRatio` provides information about the pixel density of the device. You can use this information to adjust the size or density of UI elements, such as icons or images.

### 4. OrientationBuilder Widget

The `OrientationBuilder` widget allows you to conditionally render different UI elements based on device orientation. It takes a builder function with an `Orientation` parameter, allowing you to customize the UI based on the current device orientation.

```dart
OrientationBuilder(
  builder: (BuildContext context, Orientation orientation) {
    return Container(
      child: Text(orientation.toString()),
    );
  },
)
```

## Conclusion

In this blog post, we explored how to make UI elements responsive to both landscape and portrait modes using the `MediaQuery` class in Flutter. By detecting the device orientation and adjusting the UI layout and behavior accordingly, we can ensure a consistent and seamless user experience across different orientations. So go ahead and make your app responsive to provide a delightful user experience!

#Flutter #UI #ResponsiveDesign
---
layout: post
title: "Creating adaptive breakpoints with `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [mediaquery]
comments: true
share: true
---

In Flutter, `MediaQuery` is a powerful class that allows us to access the device's screen information, such as the screen size and orientation. By utilizing `MediaQuery`, we can create adaptive layouts that adapt to different screen sizes.

One common use case of `MediaQuery` is to define adaptive breakpoints. Adaptive breakpoints are specific screen widths at which we want our layout to adjust dynamically. For example, we might want our app to display a different layout on smaller devices, like smartphones, compared to larger devices, like tablets.

To create adaptive breakpoints, we can leverage `MediaQuery` in combination with the `LayoutBuilder` widget. Let's take a look at an example:

```dart
import 'package:flutter/material.dart';

class MyAdaptiveLayout extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return LayoutBuilder(
      builder: (context, constraints) {
        if (constraints.maxWidth < 600) {
          // Display layout for smaller devices
          return Scaffold(
            appBar: AppBar(
              title: Text("Small device layout"),
            ),
            body: Center(
              child: Text("Small device content"),
            ),
          );
        } else {
          // Display layout for larger devices
          return Scaffold(
            appBar: AppBar(
              title: Text("Large device layout"),
            ),
            body: Center(
              child: Text("Large device content"),
            ),
          );
        }
      },
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: MyAdaptiveLayout(),
  ));
}
```

In the above example, we use the `LayoutBuilder` widget to rebuild our layout whenever the constraints change. `constraints.maxWidth` represents the maximum width available for the layout. We can use this value to conditionally display different layouts based on the screen size.

In this case, if the `maxWidth` is less than 600, we display the layout for smaller devices, and if it is greater or equal to 600, we display the layout for larger devices. You can adjust the breakpoints and layout logic according to your specific needs.

By using `MediaQuery` and `LayoutBuilder`, we can create adaptive breakpoints in Flutter to provide a better user experience across different devices.

#flutter #mediaquery
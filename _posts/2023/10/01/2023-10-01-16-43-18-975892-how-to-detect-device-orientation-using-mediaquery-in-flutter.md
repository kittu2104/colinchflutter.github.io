---
layout: post
title: "How to detect device orientation using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [flutter, devicelayout]
comments: true
share: true
---

In Flutter, you can easily detect the current device orientation using the `MediaQuery` class. The `MediaQuery` class provides access to the most relevant information about the device's dimensions and display properties.

To detect the device orientation, you can use the `MediaQuery.of(context).orientation` property. This property returns an enum value of `Orientation.landscape` or `Orientation.portrait` based on the device's current orientation.

Here's an example code snippet that demonstrates how to use `MediaQuery` to detect the device orientation in Flutter:

```dart
import 'package:flutter/material.dart';

class OrientationDetectorWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final orientation = MediaQuery.of(context).orientation;

    return Scaffold(
      body: Center(
        child: Text(
          'Device Orientation: ${orientation.toString().split('.').last}',
          style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
        ),
      ),
    );
  }
}

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: OrientationDetectorWidget(),
    );
  }
}
```

In this example, we create a simple Flutter widget called `OrientationDetectorWidget`. Inside the `build` method of this widget, we use `MediaQuery` to access the orientation of the current device. We then display the orientation as a text widget in the center of the screen.

By running this code, you will see the current device orientation displayed on the screen. The orientation will update dynamically as you rotate the device.

Remember, `MediaQuery` allows you to access additional information about the device such as the screen size, aspect ratio, and more. You can utilize this information to build responsive layouts and adapt your UI based on the device's properties.

#flutter #devicelayout
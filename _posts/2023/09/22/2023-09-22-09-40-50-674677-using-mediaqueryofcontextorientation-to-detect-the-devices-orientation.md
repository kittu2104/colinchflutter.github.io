---
layout: post
title: "Using `MediaQuery.of(context).orientation` to detect the device's orientation"
description: " "
date: 2023-09-22
tags: [DeviceOrientation]
comments: true
share: true
---

In Flutter, you can easily detect the orientation of the device using the `MediaQuery` class. `MediaQuery.of(context).orientation` gives you the current orientation of the device, which can be either `Orientation.portrait` or `Orientation.landscape`.

## Syntax

```dart
MediaQuery.of(context).orientation
```

## Example Usage

```dart
import 'package:flutter/material.dart';

class OrientationDetectorWidget extends StatefulWidget {
  @override
  _OrientationDetectorWidgetState createState() =>
      _OrientationDetectorWidgetState();
}

class _OrientationDetectorWidgetState extends State<OrientationDetectorWidget> {
  Orientation _orientation;

  @override
  Widget build(BuildContext context) {
    return OrientationBuilder(
      builder: (context, orientation) {
        // Update the orientation variable when the device orientation changes
        _orientation = orientation;
        return Scaffold(
          appBar: AppBar(
            title: Text("Device Orientation"),
          ),
          body: Center(
            child: Text(
              "Current Orientation: ${_orientation.toString().split('.').last}",
              style: TextStyle(
                fontSize: 20.0,
                fontWeight: FontWeight.bold,
              ),
            ),
          ),
        );
      },
    );
  }
}

void main() {
  runApp(MaterialApp(
    debugShowCheckedModeBanner: false,
    home: OrientationDetectorWidget(),
  ));
}
```

In the above example, we create a `OrientationDetectorWidget` that extends `StatefulWidget`. Inside the `_OrientationDetectorWidgetState`, we declare a `_orientation` variable of type `Orientation` to store the current device orientation.

The `build` method returns an `OrientationBuilder` widget that rebuilds the UI whenever the device orientation changes. Inside the builder function, we update the `_orientation` variable with the new orientation value.

Finally, we display the current orientation using a `Text` widget, accessed by `MediaQuery.of(context).orientation.toString().split('.').last`. The result is a string representation of the orientation value.

Make sure to wrap your app with a `MaterialApp` and run the app using the `runApp` function.

By using `MediaQuery` and `OrientationBuilder` in Flutter, you can easily detect and respond to changes in the device's orientation, allowing you to create dynamic and flexible UIs. Happy coding! #Flutter #DeviceOrientation
---
layout: post
title: "Using `MediaQuery.of(context).orientation` to detect the device's orientation"
description: " "
date: 2023-09-23
tags: []
comments: true
share: true
---

When developing mobile applications, it is important to take into account the device's orientation to provide the best user experience. In Flutter, you can easily detect the device's orientation using the `MediaQuery` class.

The `MediaQuery` class provides information about the current media, such as screen size, orientation, and pixel density. By accessing the `MediaQueryData` object, you can determine the current orientation of the device.

Here is an example of how to use `MediaQuery.of(context).orientation` to detect the device's orientation in Flutter:

```dart
import 'package:flutter/material.dart';

class OrientationDetectorWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Orientation currentOrientation = MediaQuery.of(context).orientation;

    return Scaffold(
      body: Center(
        child: Text(
          'Current Orientation: ${currentOrientation.toString()}',
          style: TextStyle(fontSize: 18),
        ),
      ),
    );
  }
}
```

In the example above, we create a `StatelessWidget` called `OrientationDetectorWidget`. In the `build` method, we use `MediaQuery.of(context).orientation` to retrieve the current orientation of the device. The `currentOrientation` variable will be of the `Orientation` enum type, either `Orientation.portrait` or `Orientation.landscape`.

We then display the current orientation inside a `Text` widget using string interpolation.

Remember to use the `MediaQuery` class inside the build method or where a `BuildContext` is available.

By detecting the device's orientation using `MediaQuery`, you can adapt your UI and provide a better user experience based on whether the device is in portrait or landscape mode.

# Conclusion

Detecting the device's orientation is essential for building responsive and user-friendly applications in Flutter. By using `MediaQuery.of(context).orientation`, you can easily determine whether the device is in portrait or landscape mode and adjust your UI accordingly.
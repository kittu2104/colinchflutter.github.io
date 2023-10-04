---
layout: post
title: "How to listen for device pixel ratio changes using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [mediquery]
comments: true
share: true
---

With the advent of various devices with different pixel densities, it has become important for developers to adapt their applications accordingly. In Flutter, we can dynamically detect changes in the device's pixel ratio using the `MediaQuery` class.

## What is the device pixel ratio?

The device pixel ratio (also known as the device pixel density) is the ratio of physical pixels to logical pixels on a device. A higher pixel ratio means that more pixels are packed within a given screen size, resulting in a higher quality and sharper display.

## Listening for pixel ratio changes

To listen for changes in the device pixel ratio, we can use the `MediaQuery` class along with a `ValueListenableBuilder`. The `ValueListenableBuilder` listens for changes in a `ValueListenable` and rebuilds the UI whenever the value changes.

Here's an example code snippet that demonstrates how to listen for pixel ratio changes using the `MediaQuery` class:

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  ValueNotifier<double> _pixelRatioNotifier;

  @override
  void initState() {
    super.initState();
    _pixelRatioNotifier = ValueNotifier(MediaQuery.of(context).devicePixelRatio);
  }

  @override
  void dispose() {
    _pixelRatioNotifier.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return ValueListenableBuilder(
      valueListenable: _pixelRatioNotifier,
      builder: (context, double pixelRatio, child) {
        // React to pixel ratio changes
        return Container(
          child: Text(
            'Current Pixel Ratio: ${_pixelRatioNotifier.value}',
            style: TextStyle(fontWeight: FontWeight.bold),
          ),
        );
      },
    );
  }
}
```

In the above code, we create a `ValueNotifier` called `_pixelRatioNotifier` and initialize it with the initial device pixel ratio. We update the `_pixelRatioNotifier` when the pixel ratio changes using the `MediaQuery` class.

Inside the `ValueListenableBuilder`, we rebuild the UI whenever the pixel ratio changes. In this example, we simply display the current pixel ratio in a `Text` widget.

## Conclusion

Knowing how to listen for changes in the device pixel ratio is essential for building responsive UIs in Flutter. By leveraging the `MediaQuery` class and the `ValueListenableBuilder`, we can dynamically adapt our application to different pixel densities, resulting in a better user experience.

#flutter #mediquery
---
layout: post
title: "How to retrieve device aspect ratio using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [aspectratio]
comments: true
share: true
---

In Flutter, you can retrieve the device aspect ratio using the `MediaQuery` widget. The device aspect ratio is important when designing layouts to ensure they are properly displayed on different devices with varying screen sizes.

Here's an example code snippet that demonstrates how to retrieve the device aspect ratio in Flutter:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Wrap your widget with the MediaQuery widget
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Device Aspect Ratio'),
        ),
        body: Builder(
          builder: (BuildContext context) {
            // Retrieve the device aspect ratio
            var deviceSize = MediaQuery.of(context).size;
            var aspectRatio = deviceSize.aspectRatio;

            return Center(
              child: Text(
                'Device Aspect Ratio: $aspectRatio',
                style: TextStyle(
                  fontSize: 24,
                  fontWeight: FontWeight.bold,
                ),
              ),
            );
          },
        ),
      ),
    );
  }
}
```

In the example above, we create a simple Flutter application with a single page that displays the device aspect ratio. We wrap our main widget with the `MediaQuery` widget to access device-specific information. Inside the `builder` method, we retrieve the device size using `MediaQuery.of(context).size` and then access the `aspectRatio` property to get the device's aspect ratio.

The aspect ratio is then displayed in the center of the screen using a `Text` widget.

By using `MediaQuery` to retrieve the device aspect ratio, you can ensure that your Flutter application's layout is responsive and properly adapts to different devices and screen sizes.

#flutter #aspectratio
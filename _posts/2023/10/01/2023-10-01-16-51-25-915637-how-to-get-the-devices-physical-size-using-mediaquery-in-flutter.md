---
layout: post
title: "How to get the device's physical size using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [mobiledevelopment]
comments: true
share: true
---

In Flutter, you can use the `MediaQuery` class to get various information about the device that the app is running on, including the physical size of the device. The physical size refers to the dimensions of the screen in physical units such as inches or millimeters.

To get the physical size of the device's screen, you can use the `MediaQuery` class along with the `size` property. Here's an example code snippet that shows how to do it:

```dart
import 'package:flutter/material.dart';

class DeviceSizeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final Size physicalSize = MediaQuery.of(context).size;

    return Scaffold(
      appBar: AppBar(
        title: Text('Device Size'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Device Physical Size:',
              style: TextStyle(fontWeight: FontWeight.bold, fontSize: 18),
            ),
            SizedBox(height: 10),
            Text(
              '${physicalSize.width} x ${physicalSize.height} inches',
              style: TextStyle(fontSize: 16),
            ),
          ],
        ),
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: DeviceSizeScreen(),
  ));
}
```

In the above code, we first import the necessary packages and define a `DeviceSizeScreen` widget. Inside the `build` method of this widget, we use `MediaQuery.of(context).size` to get the physical size of the device's screen.

We then display the device's physical size by creating a `Column` widget with two `Text` widgets. The first `Text` widget displays the label 'Device Physical Size' in bold, and the second `Text` widget displays the actual physical size of the device's screen in inches.

To run the app, we wrap the `DeviceSizeScreen` widget inside a `MaterialApp` and specify it as the home screen. Now, when you run the app, it will display the physical size of the device's screen.

Remember to import the necessary packages and replace the existing code with this example code in your Flutter project.

#flutter #mobiledevelopment
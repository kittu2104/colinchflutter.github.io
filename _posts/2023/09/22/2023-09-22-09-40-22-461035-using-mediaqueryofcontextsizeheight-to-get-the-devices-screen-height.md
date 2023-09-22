---
layout: post
title: "Using `MediaQuery.of(context).size.height` to get the device's screen height"
description: " "
date: 2023-09-22
tags: [Flutter, ScreenHeight]
comments: true
share: true
---

Here's an example of how to use `MediaQuery.of(context).size.height` to get the device's screen height in Flutter:

```dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    double screenHeight = MediaQuery.of(context).size.height;

    return Scaffold(
      appBar: AppBar(
        title: Text('Screen Height Example'),
      ),
      body: Container(
        child: Center(
          child: Text(
            'Screen Height: $screenHeight',
            style: TextStyle(fontSize: 20),
          ),
        ),
      ),
    );
  }
}
```

In this example, we have a `Scaffold` widget that displays the screen height in its body. By accessing `MediaQuery.of(context).size.height`, we assign the device's screen height to the `screenHeight` variable. We then display this value using a `Text` widget in the center of the screen.

By utilizing `MediaQuery.of(context).size.height`, you can dynamically adapt your UI based on the device's screen size. This is particularly useful for creating responsive layouts and ensuring your app looks great on devices with various screen sizes.

Remember to import the `flutter/material.dart` package to access the necessary Flutter widgets and utilities.

#Flutter #ScreenHeight
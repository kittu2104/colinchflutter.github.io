---
layout: post
title: "Utilizing `MediaQuery.of(context).size.width` to get the device's screen width"
description: " "
date: 2023-09-23
tags: [Flutter, ScreenWidth]
comments: true
share: true
---

In Flutter, you can easily retrieve the screen width using the `MediaQuery` class. Specifically, the `MediaQuery.of(context).size.width` property gives you the width of the device's screen.

Here's an example of how you can use `MediaQuery.of(context).size.width` in your Flutter app:

```dart
import 'package:flutter/material.dart';

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    double screenWidth = MediaQuery.of(context).size.width;

    return Scaffold(
      appBar: AppBar(
        title: Text('Screen Width Example'),
      ),
      body: Container(
        alignment: Alignment.center,
        child: Text(
          'The screen width is $screenWidth pixels.',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

In this code snippet, we first import the necessary packages and define a `MyHomePage` class that extends `StatelessWidget`. Inside the `build` method, we retrieve the screen width by calling `MediaQuery.of(context).size.width` and assign it to a variable named `screenWidth`.

We then use this value to display the screen width in a `Text` widget within a `Container`. The screen width is interpolated into the text string using string interpolation (`$screenWidth`).

Remember to wrap your main app widget with a `MaterialApp` and navigate to the `MyHomePage` screen to see the screen width displayed.

By utilizing `MediaQuery.of(context).size.width`, you can easily access the screen width in Flutter and dynamically adjust your UI components based on different device sizes. This ensures a consistent and responsive user experience across a variety of devices.

#Flutter #ScreenWidth
---
layout: post
title: "MediaQuery systemUIMode in Flutter"
description: " "
date: 2023-10-01
tags: [mediaquery]
comments: true
share: true
---

In Flutter, the `MediaQuery` class provides a way to query the media and the device's screen properties. One of the properties that can be queried is `systemUIMode`, which represents the current user interface mode of the operating system.

The `systemUIMode` property can be used to determine whether the device is in a light mode or a dark mode. It can be especially useful when you want to dynamically adjust your app's interface based on the current system UI mode.

To access the `systemUIMode` property, you can use the `MediaQuery.of(context)` method and then access the `systemUIMode` property of the returned `MediaQueryData` object. Here's an example of how you can use it:

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final Brightness systemUiMode = MediaQuery.of(context).platformBrightness;

    return MaterialApp(
      theme: systemUiMode == Brightness.dark
          ? ThemeData.dark()
          : ThemeData.light(),
      home: Scaffold(
        appBar: AppBar(
          title: Text("MediaQuery.systemUIMode Example"),
        ),
        body: Center(
          child: Text(
            "System UI Mode: ${systemUiMode == Brightness.dark ? 'Dark' : 'Light'}",
            style: TextStyle(fontSize: 20),
          ),
        ),
      ),
    );
  }
}
```

In the above code, we use the `systemUiMode` to determine whether the device is currently in dark mode or light mode. Based on the mode, we dynamically set the app's theme to either `ThemeData.dark()` or `ThemeData.light()`. We also display the current system UI mode as text in the center of the app's body.

Remember to import the necessary Flutter packages (`import 'package:flutter/material.dart';`) before using `MediaQuery` and `Brightness`.

By utilizing the `MediaQuery.systemUIMode` property, you can create a more responsive and visually pleasing user interface that adapts to the system UI mode of the device.

#flutter #mediaquery
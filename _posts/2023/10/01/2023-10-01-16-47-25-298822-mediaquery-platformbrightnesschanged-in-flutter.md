---
layout: post
title: "MediaQuery platformBrightnessChanged in Flutter"
description: " "
date: 2023-10-01
tags: [MediaQuery]
comments: true
share: true
---

One of the key features of Flutter is its ability to adapt to the platform it runs on. This is achieved through the use of media queries, which allow developers to retrieve information about the device's size, orientation, and other properties. Among these properties, the `platformBrightness` is particularly useful for detecting changes in the device's appearance mode, such as switching between light and dark mode.

## Introduction to platformBrightness

The `platformBrightness` property of the `MediaQueryData` class in Flutter provides information about the current brightness mode of the platform. It returns a `Brightness` enum, which can have two possible values: `Brightness.light` and `Brightness.dark`.

The `platformBrightness` property can be accessed through the `MediaQuery` class, which can be obtained using the `MediaQuery.of(context)` method. It is typically used to adapt the app's UI to the current brightness mode.

## Responding to platform brightness changes

To respond to changes in platform brightness, Flutter provides a callback called `platformBrightnessChanged`. This callback is invoked whenever the device's appearance mode changes. It can be registered using the `MediaQuery` class.

Here's an example of how to listen for platform brightness changes in a Flutter app:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  Brightness _brightness;

  @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    _brightness = MediaQuery.of(context).platformBrightness;
    WidgetsBinding.instance.addPostFrameCallback((_) {
      // Registering the callback to listen for platform brightness changes
      MediaQuery.of(context).platformBrightnessChangedCallback = () {
        setState(() {
          _brightness = MediaQuery.of(context).platformBrightness;
        });
      };
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Platform Brightness'),
      ),
      body: Center(
        child: Text(
          'Current brightness mode: ${_brightness == Brightness.light ? "Light" : "Dark"}',
          style: TextStyle(fontSize: 20),
        ),
      ),
    );
  }
}
```

In this example, we have a `MyHomePage` widget that listens for changes in platform brightness using the `platformBrightnessChangedCallback`. Whenever the brightness mode changes, it updates the `_brightness` variable and triggers a rebuild of the widget tree.

The `Text` widget inside the `Center` widget displays the current brightness mode dynamically, based on the value of `_brightness`.

## Conclusion

Being able to adapt to changes in platform brightness is essential in providing a seamless user experience. Flutter's `MediaQuery` and its `platformBrightnessChangedCallback` make it easy to respond to these changes and update the app's UI accordingly. By leveraging this feature, developers can ensure that their Flutter app looks and feels consistent across different appearance modes. #Flutter #MediaQuery
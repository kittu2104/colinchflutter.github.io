---
layout: post
title: "Handling device-specific UI adjustments using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [Flutter, UIAdjustments]
comments: true
share: true
---

When developing a mobile application using Flutter, it's important to ensure that the user interface (UI) of your app looks good and functions properly across different devices with varying screen sizes. Flutter provides the `MediaQuery` class to help handle device-specific UI adjustments seamlessly.

## What is `MediaQuery`?

`MediaQuery` is a class in Flutter that allows you to access information about the current device's media or screen properties. It provides a way to retrieve the size, orientation, and other properties of the device's screen.

## How to use `MediaQuery` for device-specific UI adjustments

Here's an example of how to use `MediaQuery` to make device-specific UI adjustments in a Flutter application:

```dart
import 'package:flutter/cupertino.dart';

class MyApp extends StatelessWidget {
  const MyApp({Key key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // Get the height and width of the current device's screen
    final double screenHeight = MediaQuery.of(context).size.height;
    final double screenWidth = MediaQuery.of(context).size.width;

    return CupertinoApp(
      title: 'My App',
      home: Scaffold(
        appBar: AppBar(
          title: Text('My App'),
        ),
        body: Container(
          height: screenHeight * 0.8,
          width: screenWidth * 0.9,
          child: Center(
            child: Text(
              'Welcome to my app!',
              style: TextStyle(fontSize: 20.0),
            ),
          ),
        ),
      ),
    );
  }
}
```

In the above example, we import the `flutter/cupertino.dart` package and use the `MediaQuery.of(context).size` property to obtain the height and width of the device's screen. We then use these values to adjust the height and width of the `Container` widget in the UI. This ensures that the UI components are rendered based on the screen size of the device.

By using `MediaQuery`, you can make your Flutter app more responsive and adaptable to different devices. It allows you to create a consistent user experience across various screen sizes, providing a better user interface for your application.

Remember to test your app on different devices and device orientations to ensure that it adapts correctly to various screen sizes and layouts.

👉 #Flutter #UIAdjustments
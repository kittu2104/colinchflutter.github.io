---
layout: post
title: "How to get the device's platform brightness using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [Flutter, Brightness]
comments: true
share: true
---

In Flutter, you can use the MediaQuery class to access the device's platform brightness. This allows you to adjust the brightness of your app's UI based on the user's preferred settings. Here's how you can retrieve the device's platform brightness in Flutter:

```dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Brightness platformBrightness = MediaQuery.of(context).platformBrightness;

    return MaterialApp(
      title: 'My App',
      theme: ThemeData(
        brightness: platformBrightness,
        // other theme properties
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('My App'),
        ),
        body: Container(
          child: Center(
            child: Text('This is my app'),
          ),
        ),
      ),
    );
  }
}

void main() {
  runApp(MyApp());
}
```

In this example, we use the `MediaQuery` class to access the `platformBrightness` property, which represents the current brightness setting of the user's device. We then pass this value to the `brightness` property of the `ThemeData` class to set the overall brightness of our app's UI.

Adjusting your app's UI based on the device's platform brightness can provide a more consistent and user-friendly experience. You can use this information to adjust the color scheme, contrast, or any other visual aspects of your app's UI elements.

Remember to import the required packages (`package:flutter/material.dart` in this case) and wrap your app's root widget with the `MaterialApp` widget to access the device's platform brightness.

By implementing this approach, you take advantage of the user's preferred brightness setting and ensure that your app's UI displays correctly and is comfortable to use in various lighting conditions.

#Flutter #UI #Brightness
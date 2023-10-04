---
layout: post
title: "How to check if the device uses dark mode using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [DarkMode]
comments: true
share: true
---

In Flutter, you can easily check if the user's device is using dark mode or light mode using the `MediaQuery` class. This allows you to adjust the appearance of your app based on the user's preference.

To determine if the device is using dark mode, you can use the `MediaQueryData.platformBrightness` property. This property will return either `Brightness.dark` or `Brightness.light`. 

Here is an example of how you can check if the device uses dark mode:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {

    Brightness currentBrightness = MediaQuery.of(context).platformBrightness;
    bool isDarkMode = currentBrightness == Brightness.dark;

    return MaterialApp(
      theme: isDarkMode ? ThemeData.dark() : ThemeData.light(),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Dark Mode Example'),
        ),
        body: Center(
          child: Text(
            isDarkMode ? 'Dark Mode' : 'Light Mode',
            style: TextStyle(fontSize: 24),
          ),
        ),
      ),
    );
  }
}
```

In this example, we first obtain the `currentBrightness` using `MediaQuery.of(context).platformBrightness` and then check if it is equal to `Brightness.dark` to determine if the device uses dark mode. We then use this information to set the appropriate theme and display the current mode on the screen.

Remember to insert the code in the appropriate place in your Flutter project and run it to see the result.

#Flutter #DarkMode
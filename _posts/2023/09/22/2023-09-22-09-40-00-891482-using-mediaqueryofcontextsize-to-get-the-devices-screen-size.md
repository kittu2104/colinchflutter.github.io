---
layout: post
title: "Using `MediaQuery.of(context).size` to get the device's screen size"
description: " "
date: 2023-09-22
tags: [MediaQuery]
comments: true
share: true
---

To get the device's screen size using MediaQuery, you can make use of the `MediaQuery.of(context).size` property. This property returns a Size object that represents the width and height of the device's screen. 

Here's an example of how you can use it in your Flutter code:

```dart
import 'package:flutter/material.dart';

class MyScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Get the screen size
    Size screenSize = MediaQuery.of(context).size;

    return Scaffold(
      appBar: AppBar(
        title: Text('Screen Size Example'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Screen Width:',
              style: TextStyle(
                fontWeight: FontWeight.bold,
              ),
            ),
            Text(
              screenSize.width.toString(),
              style: TextStyle(
                fontSize: 20.0,
              ),
            ),
            Text(
              'Screen Height:',
              style: TextStyle(
                fontWeight: FontWeight.bold,
              ),
            ),
            Text(
              screenSize.height.toString(),
              style: TextStyle(
                fontSize: 20.0,
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

In this example, we create a simple widget called `MyScreen` which displays the screen width and height in the app's UI. We retrieve the screen size using `MediaQuery.of(context).size` and display it inside `Text` widgets.

Remember to import the `flutter/material.dart` library to access the necessary Flutter widgets and classes.

By using `MediaQuery.of(context).size`, you can dynamically adjust your UI elements based on the device's screen size and provide a better user experience. It's a powerful tool for creating responsive layouts and ensuring your app looks great on all devices. 

#flutter #MediaQuery #responsivelayout
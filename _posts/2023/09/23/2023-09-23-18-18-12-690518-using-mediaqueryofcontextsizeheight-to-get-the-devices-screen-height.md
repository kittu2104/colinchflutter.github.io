---
layout: post
title: "Using `MediaQuery.of(context).size.height` to get the device's screen height"
description: " "
date: 2023-09-23
tags: [flutter, mobiledevelopment]
comments: true
share: true
---

By accessing the screen height dynamically, you can create a more responsive and user-friendly interface. Let's take a look at an example of how you can utilize this property in your Flutter app.

```dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    double screenHeight = MediaQuery.of(context).size.height;

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Screen Height Example'),
        ),
        body: Column(
          children: [
            Container(
              height: screenHeight * 0.6,
              color: Colors.blue,
              child: Center(
                child: Text(
                  'The height of this container is 60% of the screen height.',
                  style: TextStyle(color: Colors.white, fontSize: 18),
                ),
              ),
            ),
            Container(
              height: screenHeight * 0.4,
              color: Colors.green,
              child: Center(
                child: Text(
                  'The height of this container is 40% of the screen height.',
                  style: TextStyle(color: Colors.white, fontSize: 18),
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }
}

void main() {
  runApp(MyApp());
}
```

In this example, `MediaQuery.of(context).size.height` is assigned to the `screenHeight` variable. We then use this variable to set the height of two containers in the `Column` widget. The first container's height is 60% of the screen height, and the second container's height is 40% of the screen height.

By leveraging the `MediaQuery.of(context).size.height` property, you can create more flexible and adaptable layouts across different devices, ensuring a seamless user experience.

#flutter #mobiledevelopment
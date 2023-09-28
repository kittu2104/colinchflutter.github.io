---
layout: post
title: "Using `MediaQuery.of(context).size` to get the device's screen size"
description: " "
date: 2023-09-23
tags: [ResponsiveDesign]
comments: true
share: true
---

To get the width and height of the screen, we can use the following code in Flutter:

```dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final screenSize = MediaQuery.of(context).size;
    final screenWidth = screenSize.width;
    final screenHeight = screenSize.height;

    return MaterialApp(
        home: Scaffold(
            appBar: AppBar(
              title: Text('Screen Size Demo'),
            ),
            body: Center(
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[
                  Text(
                    'Screen Width: $screenWidth',
                    style: TextStyle(
                        fontWeight: FontWeight.bold, fontSize: 20),
                  ),
                  Text(
                    'Screen Height: $screenHeight',
                    style: TextStyle(
                        fontWeight: FontWeight.bold, fontSize: 20),
                  ),
                ],
              ),
            )));
  }
}

void main() {
  runApp(MyApp());
}
```

In the example code above, we create a simple Flutter app with an `AppBar` and a `Center` widget in the body. Inside the `Center` widget, we use a `Column` widget to display the screen width and height as `Text` widgets.

We access the device's screen size by calling `MediaQuery.of(context).size` and store it in the `screenSize` variable. We then extract the width and height from the `screenSize` using `screenWidth` and `screenHeight` variables, respectively.

By incorporating the device's screen size into your app's layout calculations, you can create a more responsive and user-friendly experience across different devices and screen sizes.

#Flutter #ResponsiveDesign
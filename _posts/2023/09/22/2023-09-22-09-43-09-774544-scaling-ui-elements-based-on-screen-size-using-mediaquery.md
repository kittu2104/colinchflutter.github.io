---
layout: post
title: "Scaling UI elements based on screen size using `MediaQuery`"
description: " "
date: 2023-09-22
tags: [flutter, responsivedesign]
comments: true
share: true
---

To get started, we need to import the necessary packages:

```dart
import 'package:flutter/material.dart';
```

Next, let's create a simple Flutter app with a centered button whose size scales based on the screen size:

```dart
class ScalingUIApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Scaling UI Example'),
        ),
        body: Center(
          child: Container(
            width: MediaQuery.of(context).size.width * 0.8,
            height: MediaQuery.of(context).size.height * 0.2,
            child: ElevatedButton(
              onPressed: () {},
              child: Text(
                'Click Me!',
                style: TextStyle(fontSize: 20.0),
              ),
            ),
          ),
        ),
      ),
    );
  }
}

void main() {
  runApp(ScalingUIApp());
}
```

In this example, we use the `MediaQuery` class to retrieve the screen size using `MediaQuery.of(context).size`. By multiplying it with a scale factor (0.8 for width and 0.2 for height in this case), we make the button's dimensions responsive and adapt to different screen sizes.

Note that you can adjust the scale factor to suit your needs and the layout of your UI.

With this simple approach, your UI elements can automatically scale to fit different device screen sizes and provide a consistent user experience.

#flutter #responsivedesign
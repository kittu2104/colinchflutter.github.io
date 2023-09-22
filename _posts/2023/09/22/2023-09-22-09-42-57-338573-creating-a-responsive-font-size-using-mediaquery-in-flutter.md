---
layout: post
title: "Creating a responsive font size using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [Flutter, ResponsiveDesign]
comments: true
share: true
---

In Flutter, creating a responsive user interface is essential to ensure that your app looks good on different screen sizes. One aspect of a responsive UI is having font sizes that adapt to the device's screen size.

The `MediaQuery` widget in Flutter provides information about the current device, such as screen size and orientation. By using `MediaQuery`, you can adjust the font size based on the screen dimensions.

Here's an example of how to create a responsive font size using `MediaQuery` in Flutter:

```dart
import 'package:flutter/material.dart';

class ResponsiveText extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final screenWidth = MediaQuery.of(context).size.width;
    final screenHeight = MediaQuery.of(context).size.height;

    double fontSize;

    if (screenWidth < 500) {
      // For smaller devices
      fontSize = 16.0;
    } else if (screenWidth < 1000) {
      // For medium-sized devices
      fontSize = 18.0;
    } else {
      // For larger devices
      fontSize = 20.0;
    }

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive Text'),
        ),
        body: Center(
          child: Text(
            'Hello, Flutter!',
            style: TextStyle(
              fontSize: fontSize,
              fontWeight: FontWeight.bold,
            ),
          ),
        ),
      ),
    );
  }
}

void main() {
  runApp(ResponsiveText());
}
```

In this example, we first obtain the screen width and height using `MediaQuery.of(context).size`. Then, we define different font sizes based on the screen width. For smaller devices with a width less than 500, we set the font size to 16.0. For medium-sized devices with a width less than 1000, we set the font size to 18.0. Finally, for larger devices, we set the font size to 20.0.

Inside the `Text` widget, we apply the calculated font size using the `style` property.

By using `MediaQuery` to adjust the font size based on the screen dimensions, you can ensure that your app's text remains legible and responsive across different devices.

#Flutter #ResponsiveDesign
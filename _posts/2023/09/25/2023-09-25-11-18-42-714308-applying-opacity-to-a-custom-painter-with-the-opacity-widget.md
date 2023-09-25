---
layout: post
title: "Applying opacity to a custom painter with the Opacity widget"
description: " "
date: 2023-09-25
tags: [opacity]
comments: true
share: true
---

When creating custom painted widgets in Flutter, you may want to apply different visual effects to enhance the user interface. One common effect is applying opacity to a custom painter. 

## Using the Opacity Widget

The Opacity widget in Flutter allows you to control the transparency level of its child widget. By wrapping the custom painter within the Opacity widget, you can easily apply opacity to your custom painter.

To demonstrate this, let's consider a simple example of a custom painter drawing a rectangle. We'll apply different levels of opacity to the rectangle using the Opacity widget.

```dart
import 'package:flutter/material.dart';

class MyCustomPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()
      ..color = Colors.blue
      ..style = PaintingStyle.fill;

    canvas.drawRect(Offset.zero & size, paint);
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) => false;
}


void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('Opacity Example'),
      ),
      body: Center(
        child: Opacity(
          opacity: 0.5,
          child: CustomPaint(
            painter: MyCustomPainter(),
            size: Size(200, 200),
          ),
        ),
      ),
    ),
  ));
}
```

In the code above, we define a custom painter called `MyCustomPainter` which draws a blue rectangle on the canvas. 

To apply opacity to the custom painter, we wrap it with the Opacity widget. We set the `opacity` property to 0.5, which means that the custom painter will be rendered with 50% transparency.

By running the application, you will see a blue rectangle with transparency in the center of the screen.

## Conclusion

The Opacity widget in Flutter provides an easy way to apply transparency to a custom painter. By adjusting the opacity value, you can add visual effects and enhance the user interface of your app. Experiment with different opacity levels to achieve the desired visual effect in your custom painted widgets.

#flutter #opacity #custompainter
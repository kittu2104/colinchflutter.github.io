---
layout: post
title: "Creating a custom shape divider with CustomClipper in Flutter"
description: " "
date: 2023-09-21
tags: [FlutterUI, CustomClipper]
comments: true
share: true
---

In Flutter, `CustomClipper` is a powerful tool that allows you to create and customize various shapes for your UI elements. In this tutorial, we will learn how to create a custom shape divider using `CustomClipper`.

To get started, let's create a new Flutter project and open the main.dart file. We will use a `CustomPaint` widget to create our custom shape divider.

```dart
import 'package:flutter/material.dart';

class CustomShapeDivider extends StatefulWidget {
  @override
  _CustomShapeDividerState createState() => _CustomShapeDividerState();
}

class _CustomShapeDividerState extends State<CustomShapeDivider> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Shape Divider'),
      ),
      body: Column(
        children: [
          Container(
            height: 200,
            child: CustomPaint(
              painter: DividerClipper(),
            ),
          ),
          Text('Your content goes here'),
        ],
      ),
    );
  }
}

class DividerClipper extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    Paint paint = Paint();
    paint.color = Colors.blue;
    paint.style = PaintingStyle.fill;

    Path path = Path();
    path.moveTo(0, size.height * 0.5);
    path.lineTo(size.width * 0.5, size.height * 0.8);
    path.lineTo(size.width, size.height * 0.5);
    path.lineTo(size.width, 0);
    path.lineTo(0, 0);
    path.close();

    canvas.drawPath(path, paint);
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return true;
  }
}

void main() {
  runApp(MaterialApp(
    home: CustomShapeDivider(),
  ));
}
```

In the above code, we have created a `CustomShapeDivider` widget which extends `StatefulWidget`. Inside the `build` method, we have a `Column` containing a `Container` with a `CustomPaint` widget as a child. The `paint` method in the `DividerClipper` class is responsible for creating the custom shape using the `Path` and `Canvas` classes. We draw a triangular shape from the bottom center to the top center of the container.

To use our custom shape divider, simply add the `CustomShapeDivider()` widget to your desired location in your app's UI hierarchy.

That's it! You have now successfully created a custom shape divider using `CustomClipper` in Flutter. Feel free to experiment with different paths and paint options to create unique shapes that fit your specific design requirements.

#Flutter #FlutterUI #CustomClipper
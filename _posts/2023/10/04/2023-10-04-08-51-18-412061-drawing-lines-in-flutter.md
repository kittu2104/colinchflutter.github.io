---
layout: post
title: "Drawing lines in Flutter"
description: " "
date: 2023-10-04
tags: [drawing, customizing]
comments: true
share: true
---

In Flutter, you can easily draw lines using the `CustomPaint` widget and the `Canvas` class. This allows you to create custom drawings and designs within your app. In this blog post, we will explore how to draw lines using Flutter.

## Table of Contents
- [Drawing a Line](#drawing-a-line)
- [Customizing the Line](#customizing-the-line)

## Drawing a Line

To draw a line in Flutter, you need to use the `CustomPaint` widget. This widget takes a `child` parameter, which represents the main content of the widget, and a `painter` parameter, which is responsible for drawing the line.

To draw a line, you will typically create a custom `CustomPainter` class that extends the `CustomPainter` base class. Inside this class, you will implement the `paint` method, which is where you define the drawing operations.

Here's an example of how to draw a simple horizontal line:

```dart
import 'package:flutter/material.dart';

class LinePainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()
      ..color = Colors.black
      ..strokeWidth = 2.0;

    final startPoint = Offset(0, size.height / 2);
    final endPoint = Offset(size.width, size.height / 2);

    canvas.drawLine(startPoint, endPoint, paint);
  }

  @override
  bool shouldRepaint(LinePainter oldDelegate) => false;
}

class LineWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: LinePainter(),
      child: Container(),
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      body: LineWidget(),
    ),
  ));
}
```

## Customizing the Line

You can customize the line by modifying the `Paint` object. For example, you can change the color, stroke width, or dash pattern. You can also draw different line shapes, such as dashed lines or rounded corners.

Here's an example of how to customize the line:

```dart
class LinePainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()
      ..color = Colors.blue
      ..strokeWidth = 5.0
      ..style = PaintingStyle.stroke; // Set the style to stroke for a hollow line

    final path = Path();
    path.moveTo(0, size.height / 2);
    path.lineTo(size.width, size.height / 2);

    // Draw dashed line
    final dashWidth = 15;
    final dashSpace = 10;
    final dashPaint = Paint()
      ..color = Colors.red
      ..strokeWidth = 2.0
      ..style = PaintingStyle.stroke; // Set the style to stroke for a dashed line
    canvas.drawPath(
      dashPath(path, dashArray: CircularIntervalList<double>([dashWidth, dashSpace])),
      dashPaint,
    );

    // Draw a rounded line
    final roundedPaint = Paint()
      ..color = Colors.green
      ..strokeWidth = 3.0
      ..style = PaintingStyle.stroke; // Set the style to stroke for a hollow line
    canvas.drawRRect(
      RRect.fromRectAndRadius(
        Rect.fromPoints(Offset.zero, Offset(size.width, size.height)), 
        Radius.circular(20),
      ),
      roundedPaint,
    );
  }

  @override
  bool shouldRepaint(LinePainter oldDelegate) => false;
}
```

In the above example, we have added two additional line shapes - a dashed line and a rounded line. Modify the properties of the `Paint` object to achieve the desired customization.

## Conclusion

Drawing lines in Flutter is simple and flexible thanks to the `CustomPaint` widget and the `Canvas` class. You can easily create custom line designs to suit the needs of your app. Experiment with different properties of the `Paint` object to achieve the desired visual effects.
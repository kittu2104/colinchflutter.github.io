---
layout: post
title: "Creating a signature pad with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [Flutter, CustomPainter]
comments: true
share: true
---

In this tutorial, we will learn how to create a signature pad in Flutter using the `CustomPainter` class. This will allow users to draw their signature directly on the screen.

## Setup

First, create a new Flutter project and open the main.dart file. Remove the initial code and replace it with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(SignaturePadApp());
}

class SignaturePadApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Signature Pad',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: SignaturePadScreen(),
    );
  }
}

class SignaturePadScreen extends StatefulWidget {
  @override
  _SignaturePadScreenState createState() => _SignaturePadScreenState();
}

class _SignaturePadScreenState extends State<SignaturePadScreen> {
  List<Offset> _points = <Offset>[];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Signature Pad'),
      ),
      body: GestureDetector(
        onPanUpdate: (DragUpdateDetails details) {
          setState(() {
            RenderBox renderBox = context.findRenderObject() as RenderBox;
            _points = List.from(_points)
              ..add(renderBox.globalToLocal(details.globalPosition));
          });
        },
        onPanEnd: (DragEndDetails details) => _points.add(null),
        child: CustomPaint(
          painter: SignaturePainter(_points),
          size: Size.infinite,
        ),
      ),
    );
  }
}

class SignaturePainter extends CustomPainter {
  List<Offset> points;

  SignaturePainter(this.points);

  @override
  void paint(Canvas canvas, Size size) {
    Paint paint = Paint()
      ..color = Colors.black
      ..strokeCap = StrokeCap.round
      ..strokeWidth = 5.0;

    for (int i = 0; i < points.length - 1; i++) {
      if (points[i] != null && points[i + 1] != null) {
        canvas.drawLine(points[i], points[i + 1], paint);
      }
    }
  }

  @override
  bool shouldRepaint(SignaturePainter old) => old.points != points;
}
```

## Explanation

The code above defines a Flutter application with a `SignaturePadApp` widget as the root widget. Inside `SignaturePadScreen`, we create a list of `Offset` points that represent the user's signature. 

We use a `GestureDetector` to detect the user's finger movements on the screen and update the `points` list accordingly. The `CustomPaint` widget is used to render the signature by calling the `SignaturePainter` class, which extends the `CustomPainter` class.

The `SignaturePainter` class defines the `paint` function, where we use the `Canvas` object to draw lines based on the `points` list.

## Conclusion

By implementing a `CustomPainter`, we can create a signature pad in Flutter. The user can draw their signature on the screen, and the signature will be rendered in real-time. This can be a useful feature in applications that require signatures, such as digital contracts or forms.

## #Flutter #CustomPainter
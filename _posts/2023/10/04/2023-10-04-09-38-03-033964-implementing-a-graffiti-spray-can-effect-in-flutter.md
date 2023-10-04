---
layout: post
title: "Implementing a graffiti spray can effect in Flutter"
description: " "
date: 2023-10-04
tags: [getting, creating]
comments: true
share: true
---

Graffiti art has become popular in recent years, adding vibrant and creative visuals to urban landscapes. If you're a Flutter developer looking to add some artistic flair to your application, why not try implementing a graffiti spray can effect? In this tutorial, we'll guide you through the process of creating a spray can effect using Flutter's powerful graphics capabilities.

## Table of Contents
- [Getting Started](#getting-started)
- [Creating the Spray Can](#creating-the-spray-can)
- [Implementing the Spray Effect](#implementing-the-spray-effect)
- [Interactive Painting](#interactive-painting)
- [Conclusion](#conclusion)

## Getting Started

To get started, make sure you have Flutter and Dart installed on your machine. Create a new Flutter project and open it in your favorite code editor.

## Creating the Spray Can

To create the spray can effect, we'll start by designing a custom widget that represents a spray can. This widget will include a nozzle element and a container to simulate the paint.

```dart
import 'package:flutter/material.dart';

class SprayCan extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      height: 100,
      width: 50,
      decoration: BoxDecoration(
        color: Colors.grey[300],
        borderRadius: BorderRadius.circular(10),
        boxShadow: [
          BoxShadow(
            color: Colors.grey[500],
            offset: Offset(0.0, 2.0),
            blurRadius: 6.0,
          ),
        ],
      ),
      child: Stack(
        alignment: Alignment.center,
        children: [
          Container(
            width: 20,
            height: 50,
            decoration: BoxDecoration(
              color: Colors.grey[600],
              borderRadius: BorderRadius.circular(10),
            ),
          ),
          Container(
            width: 10,
            height: 20,
            decoration: BoxDecoration(
              color: Colors.grey[600],
              borderRadius: BorderRadius.circular(10),
            ),
          ),
        ],
      ),
    );
  }
}
```

## Implementing the Spray Effect

Now that we have our spray can widget, we can move on to implementing the spray effect. We will create another custom widget called SprayPainter that listens to user touch events and paints colorful dots on the canvas.

```dart
import 'package:flutter/material.dart';
import 'dart:ui';

class SprayPainter extends StatefulWidget {
  @override
  _SprayPainterState createState() => _SprayPainterState();
}

class _SprayPainterState extends State<SprayPainter> {
  List<Offset> _points = [];

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onPanUpdate: (details) {
        setState(() {
          RenderBox renderBox = context.findRenderObject() as RenderBox;
          Offset localPosition =
              renderBox.globalToLocal(details.globalPosition);
          _points = [..._points, localPosition];
        });
      },
      onPanEnd: (details) {
        setState(() {
          _points = [];
        });
      },
      child: CustomPaint(
        painter: SprayPainterCustomPainter(_points),
      ),
    );
  }
}

class SprayPainterCustomPainter extends CustomPainter {
  final List<Offset> points;

  SprayPainterCustomPainter(this.points);

  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()
      ..color = Colors.blue
      ..strokeWidth = 3.0
      ..strokeCap = StrokeCap.round;

    for (var point in points) {
      canvas.drawCircle(point, 5.0, paint);
    }
  }

  @override
  bool shouldRepaint(SprayPainterCustomPainter oldDelegate) => true;
}
```

## Interactive Painting

To complete the implementation, let's combine our SprayCan widget and SprayPainter widget inside a Flutter app. We can add the spray can at the top and the spray painter below it. This way, the user can simulate spraying paint on the canvas by dragging their finger across the screen.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(GraffitiApp());
}

class GraffitiApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Graffiti Spray Can',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Graffiti Spray Can'),
        ),
        body: Column(
          crossAxisAlignment: CrossAxisAlignment.center,
          children: [
            Padding(
              padding: EdgeInsets.all(16.0),
              child: SprayCan(),
            ),
            Expanded(
              child: SprayPainter(),
            ),
          ],
        ),
      ),
    );
  }
}
```

## Conclusion

By following the steps outlined in this tutorial, you can now implement a graffiti spray can effect in your Flutter application. This not only adds a fun and interactive element to your app but also showcases the powerful graphics capabilities of Flutter. Experiment with different colors and brush sizes to create unique graffiti art with a touch of your finger! #Flutter #Graffiti
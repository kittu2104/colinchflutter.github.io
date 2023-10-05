---
layout: post
title: "Creating an etch-a-sketch app in Flutter"
description: " "
date: 2023-10-04
tags: [setting]
comments: true
share: true
---

In this tutorial, we will walk through the process of creating an Etch-a-Sketch app using Flutter. The Etch-a-Sketch is a classic toy that allows users to draw by turning two dials. We will build a simple version of this toy as a mobile app using the Flutter framework.

## Table of Contents
1. [Introduction](#introduction)
2. [Setting up the Project](#setting-up-the-project)
3. [Designing the UI](#designing-the-ui)
4. [Implementing the Drawing Functionality](#implementing-the-drawing-functionality)
5. [Adding Shake-to-Clear Functionality](#adding-shake-to-clear-functionality)
6. [Conclusion](#conclusion)

## Introduction <a name="introduction"></a>
Flutter is a cross-platform development framework created by Google that allows developers to build beautiful and high-performance mobile applications. We will leverage Flutter's widget-based approach to design the user interface and implement the drawing functionality of our Etch-a-Sketch app.

## Setting up the Project <a name="setting-up-the-project"></a>
To get started, make sure you have Flutter installed on your machine. You can download Flutter from the official website and follow the installation instructions.

Once Flutter is installed, open your terminal or command prompt and create a new Flutter project:

```dart
flutter create etch_a_sketch_app
cd etch_a_sketch_app
```

## Designing the UI <a name="designing-the-ui"></a>
The first step is to design the user interface for our Etch-a-Sketch app. We will use Flutter's widget system to build a canvas where users can draw.

Create a new file called `canvas.dart` in the `lib` directory. Add the following code to define the `Canvas` widget:

```dart
import 'package:flutter/material.dart';

class Canvas extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      color: Colors.white,
      child: Center(
        child: Text(
          'Start drawing!',
          style: TextStyle(
            fontSize: 24,
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  }
}
```

In the main `main.dart` file, replace the default code with the following code to use the `Canvas` widget as the app's home screen:

```dart
import 'package:flutter/material.dart';
import 'package:etch_a_sketch_app/canvas.dart';

void main() {
  runApp(EtchASketchApp());
}

class EtchASketchApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Canvas(),
    );
  }
}
```

Run the app using the `flutter run` command. You should see a white screen with the text "Start drawing!" in the center.

## Implementing the Drawing Functionality <a name="implementing-the-drawing-functionality"></a>
Now let's add the drawing functionality to our Etch-a-Sketch app. We will use Flutter's `GestureDetector` widget to detect user touch movements on the canvas and update the drawing accordingly.

In the `canvas.dart` file, replace the existing code with the following code:

```dart
import 'package:flutter/material.dart';

class Canvas extends StatefulWidget {
  @override
  _CanvasState createState() => _CanvasState();
}

class _CanvasState extends State<Canvas> {
  List<Offset> _points = [];

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onPanDown: (details) {
        setState(() {
          _points.add(details.localPosition);
        });
      },
      onPanUpdate: (details) {
        setState(() {
          _points.add(details.localPosition);
        });
      },
      onPanEnd: (details) {
        setState(() {
          _points.add(null);
        });
      },
      child: CustomPaint(
        painter: CanvasPainter(_points),
      ),
    );
  }
}

class CanvasPainter extends CustomPainter {
  final List<Offset> points;

  CanvasPainter(this.points);

  @override
  void paint(Canvas canvas, Size size) {
    Paint paint = Paint()
      ..color = Colors.black
      ..strokeWidth = 2
      ..strokeCap = StrokeCap.round;

    for (int i = 1; i < points.length; i++) {
      if (points[i - 1] != null && points[i] != null) {
        canvas.drawLine(points[i - 1], points[i], paint);
      }
    }
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return true;
  }
}
```

With this updated code, we are now able to draw on the canvas. Run the app, and you can start drawing by dragging your finger across the screen.

## Adding Shake-to-Clear Functionality <a name="adding-shake-to-clear-functionality"></a>
To make our Etch-a-Sketch app more interactive, let's add a shake-to-clear functionality. When the user shakes their device, the drawing should reset to a blank canvas.

Add the following code to the `_CanvasState` class in the `canvas.dart` file:

```dart
import 'package:sensors/sensors.dart';

@override
void initState() {
  super.initState();
  accelerometerEvents.listen((event) {
    if (event.x.abs() > 10 || event.y.abs() > 10) {
      setState(() {
        _points.clear();
      });
    }
  });
}
```

Make sure to add the `sensors` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  sensors: ^0.5.3
```

Now, when the user shakes their device, the drawing will be cleared.

## Conclusion <a name="conclusion"></a>
In this tutorial, we have created an Etch-a-Sketch app using Flutter. We learned how to design the UI, implement the drawing functionality, and add a shake-to-clear feature. Flutter's ease of use and powerful widgets make it an excellent choice for building mobile applications with rich and engaging user interfaces. Have fun exploring and enhancing the Etch-a-Sketch app further!
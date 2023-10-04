---
layout: post
title: "Implementing a graffiti wall in Flutter"
description: " "
date: 2023-10-04
tags: [graffitiwall]
comments: true
share: true
---

## Introduction
Flutter is a popular framework for building beautiful and interactive user interfaces across different platforms. In this blog post, we will explore how to create a graffiti wall using Flutter, allowing users to draw and express their creativity.

## Prerequisites
To follow along with this tutorial, you should have a basic understanding of Flutter and Dart programming language. Make sure you have Flutter installed and set up on your development environment.

## Getting Started
First, create a new Flutter project using the following command:

```shell
$ flutter create graffiti_wall
```

Change your working directory to the newly created project:

```shell
$ cd graffiti_wall
```

## Setting up the Canvas
To create the graffiti wall, we will use a `CustomPaint` widget. Create a new file called `graffiti_wall.dart` inside the `lib` directory. In this file, define a stateful widget called `GraffitiWall`:

```dart
import 'package:flutter/material.dart';

class GraffitiWall extends StatefulWidget {
  @override
  _GraffitiWallState createState() => _GraffitiWallState();
}

class _GraffitiWallState extends State<GraffitiWall> {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: CustomPaint(
        painter: _GraffitiPainter(),
      ),
    );
  }
}
```

## Creating the Painter
Next, we need to create a custom painter class to handle the drawing on the canvas. Create a new file called `graffiti_painter.dart` inside the `lib` directory. In this file, define a class called `_GraffitiPainter` that extends `CustomPainter`:

```dart
import 'package:flutter/material.dart';

class _GraffitiPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Implement your drawing logic here
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return true;
  }
}
```

## Handling User Input
To allow users to draw on the canvas, we need to handle touch events. Modify the `_GraffitiWallState` class in `graffiti_wall.dart` to include gesture detection:

```dart
import 'package:flutter/material.dart';

class _GraffitiWallState extends State<GraffitiWall> {
  List<Offset> _points = [];

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onPanUpdate: (DragUpdateDetails details) {
        setState(() {
          RenderBox renderBox = context.findRenderObject() as RenderBox;
          _points.add(renderBox.globalToLocal(details.globalPosition));
        });
      },
      onPanEnd: (DragEndDetails details) => _points.add(null),
      child: Container(
        child: CustomPaint(
          painter: _GraffitiPainter(points: _points),
        ),
      ),
    );
  }
}
```

## Drawing on the Canvas
Finally, implement the drawing logic inside the `_GraffitiPainter` class in `graffiti_painter.dart`:

```dart
import 'package:flutter/material.dart';

class _GraffitiPainter extends CustomPainter {
  List<Offset> points;

  _GraffitiPainter({this.points});

  @override
  void paint(Canvas canvas, Size size) {
    Paint paint = Paint()
      ..color = Colors.black
      ..strokeWidth = 5.0
      ..strokeCap = StrokeCap.round;

    for (int i = 0; i < points.length - 1; i++) {
      if (points[i] != null && points[i + 1] != null) {
        canvas.drawLine(points[i], points[i + 1], paint);
      }
    }
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return true;
  }
}
```

## Running the App
To see the graffiti wall in action, modify the `main.dart` file in the root directory:

```dart
import 'package:flutter/material.dart';
import 'package:graffiti_wall/graffiti_wall.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Graffiti Wall',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Graffiti Wall'),
        ),
        body: GraffitiWall(),
      ),
    );
  }
}
```

Save all the files and run the app using the following command:

```shell
$ flutter run
```

You should now see a blank canvas where you can draw on the screen by dragging your finger. Let your creativity flow on the virtual graffiti wall!

## Conclusion
In this tutorial, we learned how to implement a graffiti wall in Flutter. We explored using a `CustomPaint` widget, handling user input, and implementing custom painting logic. With these techniques, you can create interactive drawing features in your Flutter applications. Happy coding!

#flutter #graffitiwall
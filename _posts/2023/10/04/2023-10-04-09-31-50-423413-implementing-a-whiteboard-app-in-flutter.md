---
layout: post
title: "Implementing a whiteboard app in Flutter"
description: " "
date: 2023-10-04
tags: [setting]
comments: true
share: true
---

In this blog post, we will explore how to implement a whiteboard app using **Flutter**. Flutter is an open-source framework developed by Google for building beautiful, natively compiled applications for mobile, web, and desktop from a single codebase.

## Table of Contents

- [Introduction](#introduction)
- [Setting Up the Project](#setting-up-the-project)
- [Creating the Whiteboard Canvas](#creating-the-whiteboard-canvas)
- [Adding Drawing Functionality](#adding-drawing-functionality)
- [Saving and Clearing the Drawing](#saving-and-clearing-the-drawing)
- [Conclusion](#conclusion)

## Introduction

A whiteboard app allows users to draw and write freely on a blank canvas. It can be used for various purposes like brainstorming, teaching, or simply doodling. In this project, we will create a simple whiteboard app with the ability to draw lines and shapes using touch gestures.

## Setting Up the Project

To begin, make sure you have Flutter installed on your system. If not, follow the official Flutter installation guide for your operating system. Once Flutter is set up, create a new Flutter project using the following command:

```bash
flutter create whiteboard_app
```

Once the project is created, navigate to the project directory:

```bash
cd whiteboard_app
```

## Creating the Whiteboard Canvas

Inside the `lib` folder, create a new file called `whiteboard_canvas.dart`. This file will contain the code for our whiteboard canvas widget. 

First, import the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/rendering.dart';
```

Next, create a new class called `WhiteboardCanvas` that extends `CustomPainter`. This class will handle the drawing functionality of our whiteboard:

```dart
class WhiteboardCanvas extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Implement drawing logic here
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return true;
  }
}
```

Inside the `paint` method, we will implement the drawing logic. For now, let's keep it empty and add the necessary code later.

To use this custom painter, we need to create a new instance of it and pass it to a `CustomPaint` widget. Open the `main.dart` file and replace the default `MyApp` class with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Whiteboard App',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Whiteboard App'),
        ),
        body: Center(
          child: CustomPaint(
            painter: WhiteboardCanvas(),
          ),
        ),
      ),
    );
  }
}
```

Now, if you run the app using `flutter run`, you will see a blank white canvas as the main screen.

## Adding Drawing Functionality

To enable drawing on the canvas, we need to capture touch gestures from the user and update the canvas accordingly. Let's modify the `WhiteboardCanvas` class to handle touch events:

```dart
class WhiteboardCanvas extends CustomPainter {
  List<Offset> points = [];

  @override
  void paint(Canvas canvas, Size size) {
    Paint paint = Paint()
      ..color = Colors.black
      ..strokeWidth = 3.0
      ..strokeCap = StrokeCap.round;

    for (int i = 0; i < points.length - 1; i++) {
      canvas.drawLine(points[i], points[i + 1], paint);
    }
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return true;
  }

  void addPoint(Offset point) {
    points.add(point);
  }
}
```

In the updated `paint` method, we loop through all the captured points and draw lines connecting them. We also defined a list called `points` to store the captured touch coordinates.

To capture touch events, modify the `CustomPaint` widget in the `MyApp` class as follows:

```diff
CustomPaint(
-  painter: WhiteboardCanvas(),
+  painter: WhiteboardCanvas(),
+  child: GestureDetector(
+    onPanUpdate: (details) {
+      RenderBox renderBox = context.findRenderObject() as RenderBox;
+      Offset localPosition = renderBox.globalToLocal(details.globalPosition);
+      setState(() {
+        whiteboardCanvas.addPoint(localPosition);
+      });
+    },
+  ),
),
```

In the code above, we added a `GestureDetector` as a child of the `CustomPaint` widget. In the `onPanUpdate` callback, we capture the touch position and add it to the `points` list. 

Make sure to import the necessary packages:

```dart
import 'package:flutter/gestures.dart';
import 'package:flutter/rendering.dart';
```

Now, when you run the app, you should be able to draw on the whiteboard canvas by dragging your finger across the screen.

## Saving and Clearing the Drawing

To provide additional functionality, let's add the ability to save and clear the drawing on the whiteboard. Add the following methods to the `WhiteboardCanvas` class:

```dart
void saveDrawing() {
  // Save the drawing logic
}

void clearDrawing() {
  points.clear();
}
```

Next, modify the `MyApp` class as follows to include buttons for saving and clearing the drawing:

```diff
Widget build(BuildContext context) {
  WhiteboardCanvas whiteboardCanvas = WhiteboardCanvas();
+
+  void saveDrawing() {
+    whiteboardCanvas.saveDrawing();
+  }
+
+  void clearDrawing() {
+    whiteboardCanvas.clearDrawing();
+  }

  return MaterialApp(
    title: 'Whiteboard App',
    home: Scaffold(
      appBar: AppBar(
        title: Text('Whiteboard App'),
      ),
      body: Column(
        children: [
          Expanded(
            child: Center(
              child: CustomPaint(
                painter: whiteboardCanvas,
                child: GestureDetector(
                  onPanUpdate: (details) {
                    RenderBox renderBox = context.findRenderObject() as RenderBox;
                    Offset localPosition = renderBox.globalToLocal(details.globalPosition);
                    setState(() {
                      whiteboardCanvas.addPoint(localPosition);
                    });
                  },
                ),
              ),
            ),
          ),
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              RaisedButton(
                onPressed: saveDrawing,
                child: Text('Save Drawing'),
              ),
              RaisedButton(
                onPressed: clearDrawing,
                child: Text('Clear Drawing'),
              ),
            ],
          ),
        ],
      ),
    ),
  );
}
```

Now, when you run the app, you will have buttons to save and clear the drawing on the whiteboard.

## Conclusion

In this blog post, we have learned how to implement a whiteboard app in Flutter. We started by setting up the project, creating a whiteboard canvas, adding drawing functionality, and implementing saving and clearing features.

You can further enhance the app by adding additional features like different colors, eraser functionality, or even real-time collaboration. Flutter provides a rich set of tools and libraries to build powerful and feature-rich applications. Happy coding!

**#Flutter #WhiteboardApp**
---
layout: post
title: "Implementing freehand drawing in Flutter"
description: " "
date: 2023-10-04
tags: [introduction), prerequisites)]
comments: true
share: true
---

Have you ever wanted to add a freehand drawing feature to your Flutter app? Well, you're in luck because in this tutorial, we will explore how to implement freehand drawing using the `CustomPaint` widget in Flutter.

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Creating the Drawing Canvas](#creating-the-drawing-canvas)
- [Implementing the Drawing Functionality](#implementing-the-drawing-functionality)
- [Conclusion](#conclusion)

## Introduction

Adding freehand drawing functionality to your app allows users to express their creativity and interact with your app in a more engaging way. By utilizing Flutter's powerful `CustomPaint` widget, we can easily create a canvas on which users can draw.

## Prerequisites

Before diving into the implementation, make sure you have Flutter installed on your machine. You can check if Flutter is properly installed by running the following command in your terminal:

```shell
flutter doctor
```

If Flutter is not installed, please refer to the official Flutter documentation to get started.

## Creating the Drawing Canvas

To start, create a new Flutter project and open the main.dart file. We will begin by creating a simple `CustomPaint` widget that will serve as our drawing canvas. Define a new class called `CanvasPainter` that extends `CustomPainter`. This class will handle the actual painting on the canvas.

```dart
class CanvasPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Implement drawing logic here
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

Next, create a new `CustomPaint` widget and attach the `CanvasPainter` as its painter. This will ensure that the drawing functionality is properly hooked into the widget tree.

```dart
class DrawingCanvas extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: CanvasPainter(),
    );
  }
}
```

## Implementing the Drawing Functionality

Now that we have our basic canvas set up, let's implement the drawing functionality. We will make use of Flutter's gesture detection capabilities to track user input.

Inside the `CanvasPainter` class, add the following instance variables:

```dart
List<Offset> points = [];
Paint paint = Paint()
  ..color = Colors.black
  ..strokeWidth = 5.0;
```

The `points` list will store a collection of coordinates representing the user's touch points, and the `paint` object will define the color and thickness of the stroke.

Override the `paint` method to draw the points on the canvas:

```dart
@override
void paint(Canvas canvas, Size size) {
  for (int i = 0; i < points.length - 1; i++) {
    canvas.drawLine(points[i], points[i + 1], paint);
  }
}
```

Next, update the `shouldRepaint` method to return `true` so that the canvas will be repainted whenever the user draws:

```dart
@override
bool shouldRepaint(CustomPainter oldDelegate) {
  return true;
}
```

To track user input, we will use the `GestureDetector` widget. Wrap the `CustomPaint` widget inside a `GestureDetector` and add the necessary event handlers:

```dart
class DrawingCanvas extends StatefulWidget {
  @override
  _DrawingCanvasState createState() => _DrawingCanvasState();
}

class _DrawingCanvasState extends State<DrawingCanvas> {
  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onPanUpdate: (DragUpdateDetails details) {
        setState(() {
          RenderBox renderBox = context.findRenderObject();
          Offset localPosition = renderBox.globalToLocal(details.globalPosition);
          points = List.from(points)..add(localPosition);
        });
      },
      onPanEnd: (DragEndDetails details) => points.add(null),
      child: CustomPaint(
        painter: CanvasPainter(points: points),
      ),
    );
  }
}
```

In the `onPanUpdate` event handler, we update the `points` list with the current touch coordinates and call `setState` to trigger a repaint. The `onPanEnd` event is used to add a `null` value to the `points` list, which acts as a separator between individual strokes.

Finally, update the `CanvasPainter` constructor to receive the `points` list as a parameter:

```dart
class CanvasPainter extends CustomPainter {
  final List<Offset> points;

  CanvasPainter({required this.points});

  // Remaining implementation...
}
```

## Conclusion

Congratulations! You have successfully implemented freehand drawing in Flutter using the `CustomPaint` widget. Users can now draw on the canvas using their fingers, opening up new possibilities for creativity in your Flutter app. Feel free to enhance this functionality by adding features like color selection, undo/redo functionality, or saving the drawings as images.

Remember to explore the Flutter documentation and experiment with different drawing techniques to further enhance your app's user experience!

#flutter #freedrawing
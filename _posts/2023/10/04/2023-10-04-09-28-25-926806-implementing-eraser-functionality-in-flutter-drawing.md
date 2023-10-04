---
layout: post
title: "Implementing eraser functionality in Flutter drawing"
description: " "
date: 2023-10-04
tags: [setting, creating]
comments: true
share: true
---

When building a drawing app in Flutter, it's important to provide the user with the ability to erase parts of their drawing. In this tutorial, we will walk through the process of implementing an eraser functionality in a Flutter drawing app.

## Table of Contents
- [Setting Up the Project](#setting-up-the-project)
- [Creating the Drawing Canvas](#creating-the-drawing-canvas)
- [Implementing the Eraser Functionality](#implementing-the-eraser-functionality)
- [Testing the Eraser Functionality](#testing-the-eraser-functionality)
- [Conclusion](#conclusion)

## Setting Up the Project

To get started, create a new Flutter project by running the following command in your terminal:

```bash
flutter create drawing_app
cd drawing_app
```

Next, open the `lib/main.dart` file and update the `build` method to display a blank container:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(DrawingApp());
}

class DrawingApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Drawing App'),
        ),
        body: Container(),
      ),
    );
  }
}
```

## Creating the Drawing Canvas

The next step is to create a drawing canvas where users can draw and erase. We can achieve this by using a `CustomPaint` widget. Update the `body` property in the `Scaffold` widget to use the `CustomPaint` widget:

```dart
body: CustomPaint(
  painter: DrawingCanvas(),
),
```

Next, create a new `DrawingCanvas` class that extends `CustomPainter`:

```dart
class DrawingCanvas extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Implement drawing functionality here
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return true;
  }
}
```

## Implementing the Eraser Functionality

To implement the eraser functionality, we can utilize the `drawPath` method of the `Canvas` class. Add a new method called `erase` to the `DrawingCanvas` class:

```dart
void erase(PointerEvent event) {
  final path = Path()
    ..moveTo(event.localPosition.dx, event.localPosition.dy);
  
  // Apply erase visual effect (e.g., change color to white)
  final paint = Paint()
    ..color = Colors.white
    ..blendMode = BlendMode.clear
    ..strokeWidth = 20;

  canvas.drawPath(path, paint);
}
```

In the `paint` method of the `DrawingCanvas` class, update the `canvas.drawPath` call to use a `Paint` object that will erase instead of drawing:

```dart
canvas.drawPath(path, erasePaint);
```

Next, update the `onPanUpdate` method in the `DrawingApp` class to call the `erase` method when the user is erasing:

```dart
void onPanUpdate(DrawingCanvas canvas, PointerEvent event) {
  if (canvas.isErasing) {
    canvas.erase(event);
  } else {
    canvas.draw(event);
  }
}
```

## Testing the Eraser Functionality

To test the eraser functionality, we can add a button widget to the `AppBar` that toggles between drawing and erasing modes. Add a `bool` property called `isErasing` to the `DrawingCanvas` class:

```dart
bool isErasing = false;
```

Update the `appBar` property in the `Scaffold` widget to include a button that toggles the `isErasing` property:

```dart
appBar: AppBar(
  title: Text('Drawing App'),
  actions: [
    IconButton(
      icon: Icon(canvas.isErasing ? Icons.brush : Icons.eraser),
      onPressed: () {
        setState(() {
          canvas.isErasing = !canvas.isErasing;
        });
      },
    ),
  ],
),
```

## Conclusion

In this tutorial, we learned how to implement eraser functionality in a Flutter drawing app. By utilizing the `CustomPaint` widget, `Canvas`, and `Path` classes, we were able to create a drawing canvas and provide an eraser tool for users. Feel free to extend this functionality by adding advanced features such as adjusting eraser size or undo/redo functionality.

#flutter #flutterdevelopment
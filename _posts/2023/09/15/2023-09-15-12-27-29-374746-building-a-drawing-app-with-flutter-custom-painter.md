---
layout: post
title: "Building a drawing app with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [custompainter]
comments: true
share: true
---

Flutter is a popular cross-platform framework that allows developers to build beautiful and interactive user interfaces. With its customizable widgets and strong rendering capabilities, it empowers developers to create all kinds of applications, including drawing apps.

In this tutorial, we'll explore how to build a drawing app using the **Flutter Custom Painter** widget. This widget provides a canvas on which we can draw custom shapes and paths using the Flutter's powerful drawing API.

Let's get started!

## Setting Up the Project

To begin, create a new Flutter project and set up the necessary dependencies. Open your favorite text editor or IDE and create a new project with the following structure:

```dart
my_drawing_app
  |- lib
  |    |- main.dart
  |
  |- pubspec.yaml
```

In the `pubspec.yaml` file, add the `flutter_custom_paint` dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_custom_paint: ^1.0.0
```

Run `flutter pub get` in the terminal to fetch the new dependency.

## Building the Drawing Canvas

In the `main.dart` file, import the necessary packages and create a StatefulWidget named `MyDrawingApp`. This will be our main app widget.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_custom_paint/flutter_custom_paint.dart';

void main() {
  runApp(MyDrawingApp());
}

class MyDrawingApp extends StatefulWidget {
  @override
  _MyDrawingAppState createState() => _MyDrawingAppState();
}

class _MyDrawingAppState extends State<MyDrawingApp> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Drawing App'),
        ),
        body: CustomPaint(
          painter: _MyPainter(),
        ),
      ),
    );
  }
}
```

In the above code, we create a simple app with an AppBar and a `CustomPaint` widget as the body. The `CustomPaint` widget will render our custom shapes and paths.

## Implementing the Custom Painter

Next, let's create the `_MyPainter` class, which extends the `CustomPainter` class, for handling the painting logic.

```dart
class _MyPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Implement your custom painting logic here
  }

  @override
  bool shouldRepaint(_MyPainter oldDelegate) => false;
}
```

In the `paint` method, we will define our custom painting logic to draw on the `canvas` object. We will also override the `shouldRepaint` method to determine whether to repaint the canvas or not. For simplicity, we'll always return `false`.

## Adding Interactivity

To make our drawing app interactive, we can handle user gestures such as touch and drag events. We'll use the `GestureDetector` class to capture these events and update the drawing accordingly.

```dart
class _MyPainter extends CustomPainter {
  Offset? _startPosition;
  Offset? _endPosition;

  @override
  void paint(Canvas canvas, Size size) {
    // Implement your custom painting logic here
    
    if (_startPosition != null && _endPosition != null) {
      Paint paint = Paint()
        ..color = Colors.black
        ..strokeWidth = 4.0
        ..strokeCap = StrokeCap.round;
      
      canvas.drawLine(_startPosition!, _endPosition!, paint);
    }
  }

  @override
  bool shouldRepaint(_MyPainter oldDelegate) => false;
  
  void _updateDrawing(PointerEvent event) {
    setState(() {
      if (event is PointerDownEvent) {
        _startPosition = event.localPosition;
      } else if (event is PointerMoveEvent) {
        _endPosition = event.localPosition;
      } else if (event is PointerUpEvent || event is PointerCancelEvent) {
        _startPosition = null;
        _endPosition = null;
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onPanStart: (event) => _updateDrawing(event),
      onPanUpdate: (event) => _updateDrawing(event),
      onPanEnd: (event) => _updateDrawing(event),
      child: CustomPaint(
        painter: this,
      ),
    );
  }
}
```

In the updated `_MyPainter` class, we've added the `_startPosition` and `_endPosition` variables to track the initial and final touch positions. We've also modified the `paint` method to draw a line between these two positions when they are not null.

The `build` method now wraps the `CustomPaint` widget with a `GestureDetector` widget. We use various callback functions like `onPanStart`, `onPanUpdate`, and `onPanEnd` to update the touch positions and trigger repaint.

## Conclusion

Congrats! You have successfully built a simple drawing app using Flutter's Custom Painter. You can further expand on this by adding additional shapes, colors, or custom drawing tools.

In this tutorial, we covered the basics of building a drawing app with the Flutter Custom Painter widget. Remember to experiment and explore other possibilities offered by Flutter to create stunning drawing applications.

Give it a try and unleash your creativity!

#flutter #custompainter
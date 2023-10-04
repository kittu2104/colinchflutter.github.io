---
layout: post
title: "Implementing gesture recognition in Flutter drawing"
description: " "
date: 2023-10-04
tags: [setting, implementing]
comments: true
share: true
---

In this tutorial, we will explore how to implement gesture recognition in a drawing app using Flutter. Gesture recognition allows users to interact with the app by performing various gestures, such as swiping, pinching, or tapping. We will focus on recognizing the swipe gesture to clear the drawing canvas.

## Table of Contents
- [Setting up the Project](#setting-up-the-project)
- [Implementing the Drawing Canvas](#implementing-the-drawing-canvas)
- [Adding Gesture Recognition](#adding-gesture-recognition)
- [Testing the Gesture Recognition](#testing-the-gesture-recognition)
- [Conclusion](#conclusion)

## Setting up the Project
To get started, create a new Flutter project by executing the following command:

```dart
$ flutter create gesture_recognition_drawing
```

Next, navigate into the project directory:

```dart
$ cd gesture_recognition_drawing
```

Open the project in your favorite code editor and update the `pubspec.yaml` file to include the necessary dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_gesture_recognition: ^1.3.1
```

Save the file and run the command `flutter pub get` to fetch the dependencies.

## Implementing the Drawing Canvas
Now, let's implement the drawing canvas where the user can sketch. Create a new file called `drawing_canvas.dart` and add the following code:

```dart
import 'package:flutter/material.dart';

class DrawingCanvas extends StatefulWidget {
  @override
  _DrawingCanvasState createState() => _DrawingCanvasState();
}

class _DrawingCanvasState extends State<DrawingCanvas> {
  List<Offset> _points = [];

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onPanUpdate: (details) {
        setState(() {
          RenderBox renderBox = context.findRenderObject() as RenderBox;
          _points.add(renderBox.globalToLocal(details.globalPosition));
        });
      },
      onPanEnd: (_) => _points.clear(),
      child: CustomPaint(
        painter: DrawingPainter(_points),
        child: Container(),
      ),
    );
  }
}

class DrawingPainter extends CustomPainter {
  final List<Offset> points;

  DrawingPainter(this.points);

  @override
  void paint(Canvas canvas, Size size) {
    Paint paint = Paint()
      ..color = Colors.black
      ..strokeCap = StrokeCap.round
      ..strokeWidth = 3.0;

    for (int i = 0; i < points.length - 1; i++) {
      if (points[i] != null && points[i + 1] != null) {
        canvas.drawLine(points[i], points[i + 1], paint);
      }
    }
  }

  @override
  bool shouldRepaint(DrawingPainter oldDelegate) => true;
}
```

The `DrawingCanvas` widget is responsible for rendering the canvas where the user can draw. We use `GestureDetector` to handle the user's touch interactions. The `_points` list stores the drawing coordinates, and we update it whenever the user moves their finger on the canvas. The `DrawingPainter` class handles the actual drawing of lines based on the captured coordinates.

## Adding Gesture Recognition
To clear the drawing canvas with a swipe gesture, we need to add gesture recognition to the `DrawingCanvas` widget. Update the `_DrawingCanvasState` class as follows:

```dart
import 'package:flutter_gesture_recognition/flutter_gesture_recognition.dart';

class _DrawingCanvasState extends State<DrawingCanvas> {
  List<Offset> _points = [];

  Recognizer _recognizer = Recognizer();
  Gesture _gesture = Gesture();

  @override
  void initState() {
    super.initState();

    _recognizer.onSwipeDetected = () {
      setState(() => _points.clear());
    };
  }

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onPanUpdate: (details) {
        RenderBox renderBox = context.findRenderObject() as RenderBox;
        _points.add(renderBox.globalToLocal(details.globalPosition));

        _gesture.addPoint(details.globalPosition.dx, details.globalPosition.dy);
        _recognizer.detect(_gesture);
      },
      onPanEnd: (_) {
        _gesture.stop();
        _recognizer.reset();
      },
      child: CustomPaint(
        painter: DrawingPainter(_points),
        child: Container(),
      ),
    );
  }
}
```

We initialize a `Recognizer` object and attach a function to the `onSwipeDetected` event. In the `build` method, we add the current touch point to the gesture recognizer and detect the gesture using `_recognizer.detect(_gesture)`. When the swipe gesture is detected, we clear the points list to clear the canvas.

## Testing the Gesture Recognition
To test the gesture recognition, we need to display the `DrawingCanvas` in our app. Open the default `main.dart` file and replace the contents with the following code:

```dart
import 'package:flutter/material.dart';
import 'drawing_canvas.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Gesture Recognition Drawing',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Gesture Recognition Drawing'),
        ),
        body: Center(child: DrawingCanvas()),
      ),
    );
  }
}
```

Save the file and run the app using the command `flutter run`. You should see the drawing canvas, and if you swipe your finger across the screen, the canvas should clear.

## Conclusion
In this tutorial, we explored how to implement gesture recognition in a drawing app using Flutter. We learned how to use the `flutter_gesture_recognition` package to detect swipe gestures and clear the drawing canvas accordingly. With this knowledge, you can now enhance your Flutter apps with various gesture-based interactions. Have fun experimenting with gestures in your own projects!
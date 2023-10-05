---
layout: post
title: "Creating a paint app in Flutter"
description: " "
date: 2023-10-04
tags: [setting]
comments: true
share: true
---

In this tutorial, we will learn how to create a paint app using Flutter, a cross-platform framework for building mobile applications. 

## Table of Contents
1. [Introduction](#introduction)
2. [Setting Up the Project](#setting-up-the-project)
3. [Creating the Canvas](#creating-the-canvas)
4. [Drawing on the Canvas](#drawing-on-the-canvas)
5. [Adding Color Selection](#adding-color-selection)
6. [Saving and Sharing](#saving-and-sharing)
7. [Conclusion](#conclusion)

## Introduction<a name="introduction"></a>
A paint app allows users to draw on a canvas using different tools and colors. Flutter provides several widgets and APIs that make it easy to implement this functionality.

## Setting Up the Project<a name="setting-up-the-project"></a>
Before we start building the paint app, we need to set up a new Flutter project. Follow these steps:

1. Open your terminal or command prompt.
2. Create a new Flutter project with the following command:
   ```bash
   flutter create paint_app
   ```
3. Navigate to the project folder:
   ```bash
   cd paint_app
   ```
4. Open the project in your preferred IDE or text editor.

## Creating the Canvas<a name="creating-the-canvas"></a>
To create the canvas for drawing, we will use the `CustomPaint` widget in Flutter. This widget allows us to create a custom render object and paint on it. 

```dart
import 'package:flutter/material.dart';

class DrawingCanvas extends StatefulWidget {
  @override
  _DrawingCanvasState createState() => _DrawingCanvasState();
}

class _DrawingCanvasState extends State<DrawingCanvas> {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: _CanvasPainter(),
    );
  }
}

class _CanvasPainter extends CustomPainter {
  // Implement the paint method here
  @override
  void paint(Canvas canvas, Size size) {
    // Add your drawing code here
  }
  
  // Implement the shouldRepaint method here
  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
      return false;
  }
}
```
## Drawing on the Canvas<a name="drawing-on-the-canvas"></a>
To allow users to draw on the canvas, we need to handle touch events and update the canvas accordingly. We can use the `GestureDetector` widget in Flutter to capture touch events and update the canvas.

```dart
class _DrawingCanvasState extends State<DrawingCanvas> {

  List<Offset> _points = [];

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onPanUpdate: (DragUpdateDetails details) {
        setState(() {
          RenderBox renderBox = context.findRenderObject() as RenderBox;
          Offset localPosition =
              renderBox.globalToLocal(details.globalPosition);
          _points = List.from(_points)..add(localPosition);
        });
      },
      onPanEnd: (DragEndDetails details) {
        setState(() {
          _points.add(null);
        });
      },
      child: CustomPaint(
        painter: _CanvasPainter(points: _points),
      ),
    );
  }
}
```

## Adding Color Selection<a name="adding-color-selection"></a>
To allow users to select different colors for drawing, we can use the `ColorPicker` widget from the `flutter_colorpicker` package. 

First, add the package to your `pubspec.yaml` file:
```yaml
dependencies:
  flutter_colorpicker: ^0.5.1
```
Then, import the package and add a color picker as a child widget in the paint app:
```dart
import 'package:flutter_colorpicker/flutter_colorpicker.dart';

class PaintApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Paint App'),
          backgroundColor: Colors.blue,
        ),
        body: Column(
          children: [
            ColorPicker(
              pickerColor: pickerColor, // Set the color initially
              onColorChanged: (color) {
                // Handle color changed event
              },
            ),
            DrawingCanvas(),
          ],
        ),
      ),
    );
  }
}

```

## Saving and Sharing<a name="saving-and-sharing"></a>
To allow users to save and share their artwork, we can use the `path_provider` and `share` packages in Flutter. First, add the packages to your `pubspec.yaml` file:
```yaml
dependencies:
  path_provider: ^2.0.5
  share: ^2.0.4
```

Then, import the packages, and add save and share functionality to your paint app:

```dart
import 'package:path_provider/path_provider.dart';
import 'package:share/share.dart';

class PaintApp extends StatelessWidget {
  
  // ...

  Future<void> _saveImage() async {
    RenderRepaintBoundary boundary =
        globalKey.currentContext.findRenderObject() as RenderRepaintBoundary;
    ui.Image image = await boundary.toImage();
    final directory = await getTemporaryDirectory();
    final imagePath = '${directory.path}/drawing.png';
    final byteData = await image.toByteData(format: ui.ImageByteFormat.png);
    final pngBytes = byteData.buffer.asUint8List();
    await File(imagePath).writeAsBytes(pngBytes);
  }

  void _shareImage(String imagePath) {
    Share.shareFiles([imagePath]);
  }

  @override
  Widget build(BuildContext context) {
    // ...
    return MaterialApp(
      home: Scaffold(
        // ...
        appBar: AppBar(
            // ...
            actions: [
              IconButton(
                icon: Icon(Icons.save),
                onPressed: () {
                  _saveImage();
                },
              ),
              IconButton(
                icon: Icon(Icons.share),
                onPressed: () {
                  _shareImage(imagePath);
                },
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

## Conclusion<a name="conclusion"></a>
You have learned how to create a paint app in Flutter with drawing functionality, color selection, and saving and sharing options. Feel free to customize the app further by adding additional features like different brush sizes, undo/redo functionality, or even implementing more advanced drawing techniques. Happy coding! 

#flutter #paintapp
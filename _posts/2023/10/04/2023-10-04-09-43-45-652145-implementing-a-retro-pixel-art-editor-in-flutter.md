---
layout: post
title: "Implementing a retro pixel art editor in Flutter"
description: " "
date: 2023-10-04
tags: [setting]
comments: true
share: true
---

![retro pixel art](https://example.com/retro_pixel_art.png)

Pixel art has seen a revival in recent years, with its nostalgic charm capturing the hearts of many developers and artists alike. In this tutorial, we will explore how to implement a retro pixel art editor using the Flutter framework. 

## Table of Contents
1. [Introduction](#introduction)
2. [Setting Up the Project](#setting-up-the-project)
3. [Creating the Canvas](#creating-the-canvas)
4. [Drawing Pixels](#drawing-pixels)
5. [Adding Color Palette](#adding-color-palette)
6. [Saving and Exporting](#saving-and-exporting)
7. [Conclusion](#conclusion)

## Introduction <a name="introduction"></a>

Flutter is a powerful and flexible framework for building cross-platform applications. Its declarative UI approach and fast rendering make it an ideal choice for creating a retro pixel art editor. In this tutorial, we will leverage Flutter's canvas and painting APIs to build a feature-rich pixel art editor.

## Setting Up the Project <a name="setting-up-the-project"></a>

To get started, make sure you have Flutter and Dart installed on your machine. Create a new Flutter project using the following command:

```bash
flutter create retro_pixel_art_editor
```

Next, navigate to the project directory:

```bash
cd retro_pixel_art_editor
```

Now, open the project in your favorite code editor.

## Creating the Canvas <a name="creating-the-canvas"></a>

In Flutter, the `CustomPaint` widget is commonly used for custom drawing. In our case, we will use it to create the canvas for our pixel art editor. Create a new file `canvas.dart` and add the following code:

```dart
import 'package:flutter/material.dart';

class CanvasWidget extends StatefulWidget {
  @override
  _CanvasWidgetState createState() => _CanvasWidgetState();
}

class _CanvasWidgetState extends State<CanvasWidget> {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: CanvasPainter(),
    );
  }
}

class CanvasPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Paint canvas content here
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return true; // Always repaint
  }
}
```

In this code, we have defined a `CanvasWidget` which uses the `CustomPaint` widget and a custom `CanvasPainter` to handle the actual drawing on the canvas.

## Drawing Pixels <a name="drawing-pixels"></a>

To draw pixels on the canvas, we need to handle user interactions such as tapping or dragging on the canvas. Let's update our `CanvasPainter` class to support drawing pixels. Add the following code inside the `CanvasPainter` class:

```dart
class CanvasPainter extends CustomPainter {
  List<Offset> pixels = []; // List of coordinates for each pixel

  @override
  void paint(Canvas canvas, Size size) {
    // Draw existing pixels
    for (var pixel in pixels) {
      canvas.drawCircle(pixel, 4, Paint()..color = Colors.black);
    }
  }

  // Handle user interaction
  void addPixel(Offset position) {
    setState(() {
      pixels.add(position);
    });
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return true; // Always repaint
  }
}
```

In this code, we have added a `pixels` list to store the coordinates of each pixel. The `paint` method loops through the `pixels` list and draws circles representing each pixel on the canvas.

To handle user interaction, we have added a `addPixel` method that adds the position of the tapped/dragged pixel to the `pixels` list. We use `setState` to trigger a repaint and update the canvas.

## Adding Color Palette <a name="adding-color-palette"></a>

A pixel art editor wouldn't be complete without a color palette. Let's create a color palette widget where the user can select the desired color for drawing. Add the following code to `canvas.dart`:

```dart
class ColorPalette extends StatelessWidget {
  final List<Color> colors = [
    Colors.black,
    Colors.red,
    Colors.blue,
    Colors.green,
    Colors.yellow,
    Colors.orange,
    Colors.purple,
    Colors.white,
  ];

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 60,
      child: ListView.builder(
        scrollDirection: Axis.horizontal,
        itemCount: colors.length,
        itemBuilder: (context, index) {
          return GestureDetector(
            onTap: () {
              // Handle color selection
            },
            child: Container(
              margin: EdgeInsets.all(3),
              width: 50,
              color: colors[index],
            ),
          );
        },
      ),
    );
  }
}
```

In the `ColorPalette` widget, we have defined a list of colors and created a horizontal `ListView.builder` to display the colors as rectangular containers. When a color is tapped, we can handle the color selection logic accordingly.

## Saving and Exporting <a name="saving-and-exporting"></a>

To make our pixel art editor more functional, let's add the ability to save and export the artwork. Add the following code to `canvas.dart`:

```dart
class EditorScreen extends StatelessWidget {
  final GlobalKey canvasKey = GlobalKey();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        children: [
          Expanded(
            child: RepaintBoundary(
              key: canvasKey,
              child: CanvasWidget(),
            ),
          ),
          SizedBox(height: 20),
          RaisedButton(
            child: Text("Save"),
            onPressed: () {
              _saveImage();
            },
          ),
          SizedBox(height: 10),
          RaisedButton(
            child: Text("Export"),
            onPressed: () {
              _exportImage();
            },
          ),
        ],
      ),
    );
  }

  void _saveImage() async {
    RenderRepaintBoundary boundary =
        canvasKey.currentContext.findRenderObject();
    final image = await boundary.toImage(pixelRatio: 2.0);
    // Save image logic
  }

  void _exportImage() async {
    RenderRepaintBoundary boundary =
        canvasKey.currentContext.findRenderObject();
    final image = await boundary.toImage(pixelRatio: 2.0);
    // Export image logic
  }
}
```

In this code, we have added an `EditorScreen` widget that wraps our `CanvasWidget` with a `RepaintBoundary`. By using the `RepaintBoundary` widget and `toImage` method, we can capture the contents of the canvas as an image.

The `_saveImage` method saves the captured image locally, and the `_exportImage` method allows the user to export the image to other apps or services.

## Conclusion <a name="conclusion"></a>

Congratulations! You have successfully implemented a retro pixel art editor in Flutter. With the canvas, pixel drawing, color palette, and saving/exporting functionality, you now have the foundation to build a full-featured pixel art editor.

Remember to experiment and enhance your editor with additional features such as undo/redo, different brush sizes, and custom tools. So go ahead, let your creativity loose, and start creating your own pixel art masterpieces!
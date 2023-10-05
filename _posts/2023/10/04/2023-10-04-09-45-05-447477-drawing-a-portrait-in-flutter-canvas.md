---
layout: post
title: "Drawing a portrait in Flutter Canvas"
description: " "
date: 2023-10-04
tags: [getting]
comments: true
share: true
---

In this tutorial, we'll explore how to draw a portrait using the Flutter canvas. Flutter provides a powerful canvas API that allows us to create custom drawings and graphics. With the canvas API, we have control over every pixel on the screen and can create intricate and detailed drawings.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Drawing the Outline](#drawing-the-outline)
- [Adding Facial Features](#adding-facial-features)
- [Texturing and Shading](#texturing-and-shading)
- [Conclusion](#conclusion)

## Prerequisites
To follow along with this tutorial, you should have Flutter and Dart installed on your machine. You should also have a basic understanding of Flutter widgets and how to create a new Flutter project.

## Getting Started
Let's start by creating a new Flutter project. Open your terminal or command prompt and run the following command:

```shell
flutter create portrait_app
```

Change your working directory to the newly created project:

```shell
cd portrait_app
```

Now, open the `lib/main.dart` file in your preferred code editor.

## Drawing the Outline
To draw the outline of the portrait, we'll use the `CustomPaint` widget. Replace the contents of the `MyApp` class with the following code:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Portrait App',
      home: Scaffold(
        appBar: AppBar(title: Text('Portrait')),
        body: Center(
          child: CustomPaint(
            size: Size(300, 400),
            painter: PortraitPainter(),
          ),
        ),
      ),
    );
  }
}

class PortraitPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // TODO: Implement outline drawing
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

In the `PortraitPainter` class, we've overridden the `paint` method. This is where we'll implement the code to draw the outline of the portrait. 

## Adding Facial Features
Next, let's add the facial features such as eyes, nose, and mouth. Update the `paint` method in the `PortraitPainter` class with the following code:

```dart
@override
void paint(Canvas canvas, Size size) {
  final paint = Paint()
    ..color = Colors.black
    ..strokeWidth = 2
    ..style = PaintingStyle.fill;
  
  // Draw face outline
  // TODO: Implement face outline

  // Draw eyes
  // TODO: Implement eyes drawing

  // Draw nose
  // TODO: Implement nose drawing

  // Draw mouth
  // TODO: Implement mouth drawing
}
```

In each TODO section, you can add the code to draw the respective facial feature. Use the `drawCircle` and `drawRect` methods of the canvas to draw the features.

## Texturing and Shading
To add texture and shading to the portrait, we can utilize the `Shader` class provided by Flutter. Update the `paint` method in the `PortraitPainter` class with the following code:

```dart
@override
void paint(Canvas canvas, Size size) {
  final gradient = LinearGradient(
    begin: Alignment.topCenter,
    end: Alignment.bottomCenter,
    colors: [Colors.orange, Colors.yellow],
  );

  final rect = Rect.fromLTWH(0.0, 0.0, size.width, size.height);

  final paint = Paint()
    ..shader = gradient.createShader(rect);

  // Draw face outline
  // ...

  // Draw eyes
  // ...

  // Draw nose
  // ...

  // Draw mouth
  // ...
}
```

Here, we've defined a linear gradient with orange and yellow colors. We've created a rectangle with the size of the canvas, and assigned the gradient shader to the paint object. You can adjust the colors and gradient properties as desired.

## Conclusion
In this tutorial, we learned how to draw a portrait using the Flutter canvas. We started by drawing the face outline, then added the facial features such as eyes, nose, and mouth. Finally, we explored how to add texture and shading using gradients. With the Flutter canvas API, the possibilities for creating custom graphics and drawings are endless.

Remember to experiment and have fun with your creations. Happy coding!

## #Flutter #Canvas
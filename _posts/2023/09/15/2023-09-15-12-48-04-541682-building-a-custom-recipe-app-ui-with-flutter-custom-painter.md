---
layout: post
title: "Building a custom recipe app UI with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [flutter, custompainter]
comments: true
share: true
---

In this tutorial, we will explore how to create a custom user interface for a recipe app using Flutter's `CustomPainter` class. The `CustomPainter` class allows us to draw custom shapes and widgets on a `Canvas`, giving us full control over the UI design.

## Prerequisites
- Basic knowledge of Flutter and Dart programming language
- Flutter SDK installed on your machine

## Setting up the Project

Let's start by creating a new Flutter project. Open your terminal and run the following command:

```bash
flutter create recipe_app
cd recipe_app
```

Open the project in your favorite code editor. Let's create a new file called `recipe_app.dart` and define our main application widget.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(RecipeApp());
}

class RecipeApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Recipe App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: RecipeScreen(),
    );
  }
}

class RecipeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Recipes'),
      ),
      body: Container(
        child: CustomPaint(
          painter: RecipePainter(),
          child: Center(
            child: Text('Custom Recipe UI'),
          ),
        ),
      ),
    );
  }
}
```

In the above code, we have defined our main application widget `RecipeApp`. It sets up the `MaterialApp` and defines the `RecipeScreen` as the home screen. Inside the `RecipeScreen`, we have a `Container` with a `CustomPaint` widget. The `CustomPaint` widget takes a `painter` property, which we will define next.

## Creating the Custom Painter

Create a new file called `recipe_painter.dart` and add the following code:

```dart
import 'package:flutter/material.dart';

class RecipePainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // TODO: Implement custom painting logic
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) => false;
}
```

In the `RecipePainter` class, we need to override two methods: `paint` and `shouldRepaint`. The `paint` method is where we define our custom painting logic. The `shouldRepaint` method tells Flutter if the `CustomPainter` should repaint when the widget changes.

## Adding Custom Painting Logic

Let's start by drawing a background color for our recipe app. Update the `paint` method in `recipe_painter.dart` as follows:

```dart
@override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()
      ..color = Colors.yellow
      ..style = PaintingStyle.fill;

    canvas.drawRect(Offset.zero & size, paint);
  }
```

In the above code, we create an instance of `Paint` and set the color to yellow. We then use the `drawRect` method to draw a rectangle covering the entire `Canvas` size.

Now, if you run the application, you should see a yellow background. 

## Conclusion

In this tutorial, we explored how to create a custom recipe app UI using Flutter's `CustomPainter` class. We created the main application widget, set up the home screen with a `CustomPaint` widget, and implemented a basic custom painting logic to draw a colored background. You can further enhance the UI by adding more custom drawing operations to the `paint` method.

#flutter #custompainter
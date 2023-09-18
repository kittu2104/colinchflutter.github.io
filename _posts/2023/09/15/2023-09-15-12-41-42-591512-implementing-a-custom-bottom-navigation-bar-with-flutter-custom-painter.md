---
layout: post
title: "Implementing a custom bottom navigation bar with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [CustomPainter]
comments: true
share: true
---

Before we begin, make sure you have Flutter and Dart installed on your machine. If you haven't set up Flutter yet, you can follow the instructions in the [official documentation](https://flutter.dev/docs/get-started/install).

Now let's get started with creating a new Flutter project:

1. Open a terminal or command prompt and navigate to the directory where you want to create your project.
2. Run the following command to create a new Flutter project:

```bash
flutter create custom_bottom_navigation
```

3. Change to the project directory:

```bash
cd custom_bottom_navigation
```

4. Open the project in your favorite code editor.

Now that we have a new Flutter project set up, let's create a new file called `custom_bottom_navigation.dart` inside the `lib` folder. This file will contain our custom bottom navigation bar implementation.

In `custom_bottom_navigation.dart`, we first need to import the necessary Flutter dependencies:

```dart
import 'package:flutter/material.dart';
```

Next, we'll create a new class called `CustomBottomNavigation` that extends the `StatelessWidget` class:

```dart
class CustomBottomNavigation extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      // Implement your custom bottom navigation bar UI here
    );
  }
}
```

Inside the `build` method, we'll return a `Container` widget. This is where we'll implement our custom bottom navigation bar UI. Let's start by adding a horizontal `Row` widget to hold our navigation items:

```dart
class CustomBottomNavigation extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Row(
        children: [
          // Add your navigation items here
        ],
      ),
    );
  }
}
```

Next, we'll add individual navigation items as `FlatButton` widgets inside the `Row`. You can customize these navigation items based on your app's design and requirements:

```dart
class CustomBottomNavigation extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Row(
        children: [
          FlatButton(
            onPressed: () {
              // Handle navigation to the first screen
            },
            child: Text('Screen 1'),
          ),
          FlatButton(
            onPressed: () {
              // Handle navigation to the second screen
            },
            child: Text('Screen 2'),
          ),
          FlatButton(
            onPressed: () {
              // Handle navigation to the third screen
            },
            child: Text('Screen 3'),
          ),
        ],
      ),
    );
  }
}
```

At this point, we have a basic bottom navigation bar UI set up. However, it still lacks the styling and visual indicators for the active screen. To add a custom design, we can utilize Flutter's `CustomPainter` class.

Inside the `CustomBottomNavigation` class, let's create a new method called `_drawBackground()`:

```dart
void _drawBackground(Canvas canvas, Size size) {
  // Implement the custom background drawing here
}
```

In this method, we'll use the provided `Canvas` and `Size` parameters to draw the background of our bottom navigation bar. We can use Flutter's painting API to draw shapes, gradients, and more.

For example, let's draw a simple rectangle as the background:

```dart
void _drawBackground(Canvas canvas, Size size) {
  final backgroundPaint = Paint()..color = Colors.blue;
  final backgroundRect = Rect.fromLTWH(0, 0, size.width, size.height);
  canvas.drawRect(backgroundRect, backgroundPaint);
}
```

Back in the `build` method, we'll wrap our `Container` with a `CustomPaint` widget and provide the `CustomPainter` implementation:

```dart
class CustomBottomNavigation extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: _BottomNavigationPainter(),
      child: Container(
        child: Row(
          children: [
            // Add your navigation items here
          ],
        ),
      ),
    );
  }
}
```

Finally, let's create the `_BottomNavigationPainter` class that extends `CustomPainter` and implements our custom background drawing:

```dart
class _BottomNavigationPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final backgroundPaint = Paint()..color = Colors.blue;
    final backgroundRect = Rect.fromLTWH(0, 0, size.width, size.height);
    canvas.drawRect(backgroundRect, backgroundPaint);
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return false;
  }
}
```

In the `paint` method, we'll call our `_drawBackground` method to draw the custom background. We also override the `shouldRepaint` method to avoid unnecessary repaints for performance improvements.

Congratulations! You've implemented a custom bottom navigation bar using Flutter's Custom Painter.

To use your custom bottom navigation bar, you can simply add it to your app's main widget tree. For example, you can add it inside the `Scaffold` widget's `bottomNavigationBar` property.

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Custom Bottom Navigation'),
        ),
        body: Center(
          child: Text('Hello World'),
        ),
        bottomNavigationBar: CustomBottomNavigation(),
      ),
    );
  }
}
```

Remember to replace the existing `body` property with your actual app content.

Now you have the foundation to create a custom bottom navigation bar tailored to your app's design. Feel free to experiment with different shapes, animations, and interactions to make it unique and engaging for your users.

#Flutter #CustomPainter
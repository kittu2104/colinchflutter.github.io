---
layout: post
title: "Drawing using mathematical formulas in Flutter"
description: " "
date: 2023-10-04
tags: [drawing, mathematical]
comments: true
share: true
---

In Flutter, you have the ability to create complex and visually appealing graphics by utilizing mathematical formulas. This allows you to create custom shapes, curves, and animations, giving your app a unique and artistic touch. In this blog post, we will explore how to harness the power of mathematical formulas to create stunning drawings in Flutter.

## Getting started

Before we dive into the code, make sure you have Flutter installed and set up on your machine. You can download Flutter and follow the installation instructions from the official Flutter website.

## Creating a custom widget

To draw using mathematical formulas, we need to create a custom widget that extends the `CustomPainter` class. This class allows us to define how to paint on the canvas using the `paint` method.

```dart
import 'package:flutter/material.dart';

class FormulaPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Code to paint using mathematical formulas
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

## Implementing the paint method

Inside the `paint` method, we can implement the mathematical formulas to draw our desired shapes. Let's start with a simple example of drawing a circle.

```dart
@override
void paint(Canvas canvas, Size size) {
  final center = Offset(size.width / 2, size.height / 2);
  final radius = size.width / 4;
  final paint = Paint()..color = Colors.blue;

  canvas.drawCircle(center, radius, paint);
}
```

In this example, we calculate the center point of the canvas by dividing the width and height by 2. We then define the radius of the circle using a fraction of the canvas width. Finally, we create a `Paint` object and set its color to blue. We use the `canvas.drawCircle` method to paint the circle on the canvas.

## Adding animation

To make our drawing more dynamic, we can add animation using Flutter's animation library. Let's modify our previous example to create an animated expanding circle.

```dart
class AnimatedCircle extends StatefulWidget {
  @override
  _AnimatedCircleState createState() => _AnimatedCircleState();
}

class _AnimatedCircleState extends State<AnimatedCircle>
    with SingleTickerProviderStateMixin {
  late AnimationController _animationController;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _animationController =
        AnimationController(vsync: this, duration: Duration(seconds: 2));
    _animation = Tween<double>(begin: 0, end: 300).animate(_animationController)
      ..addListener(() {
        setState(() {});
      });

    _animationController.repeat(reverse: true);
  }

  @override
  void dispose() {
    _animationController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: AnimatedPainter(animationValue: _animation.value),
    );
  }
}

class AnimatedPainter extends CustomPainter {
  final double animationValue;

  AnimatedPainter({required this.animationValue});

  @override
  void paint(Canvas canvas, Size size) {
    final center = Offset(size.width / 2, size.height / 2);
    final radius = animationValue;
    final paint = Paint()..color = Colors.blue;

    canvas.drawCircle(center, radius, paint);
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

In this modified example, we create a `StatefulWidget` called `AnimatedCircle` with an `AnimationController` and an animation object. We define the animation duration and the animation value range using a `Tween` object. The animation value is then updated in a listener attached to the animation. Finally, we use a `CustomPaint` widget to paint the animated circle, and the animation value is passed to the `AnimatedPainter` to update the radius of the circle.

## Conclusion

By leveraging the power of mathematical formulas, you can create visually stunning drawings and animations in Flutter. Whether you're drawing simple shapes or complex curves, understanding the math behind the scenes can help you unleash your creativity. So go ahead, dive into the world of mathematical drawing in Flutter and let your imagination run wild!

#flutter #drawing #mathematical-formulas
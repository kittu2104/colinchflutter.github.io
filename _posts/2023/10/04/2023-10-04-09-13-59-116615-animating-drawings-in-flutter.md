---
layout: post
title: "Animating drawings in Flutter"
description: " "
date: 2023-10-04
tags: [introduction), drawing]
comments: true
share: true
---

Flutter is a powerful framework for building cross-platform applications. One of its key features is the ability to create fluid and interactive user interfaces. In this blog post, we will explore how to animate drawings in Flutter using the `CustomPainter` class.

## Table of Contents
- [Introduction](#introduction)
- [Drawing Shapes](#drawing-shapes)
- [Animating Drawings](#animating-drawings)
- [Conclusion](#conclusion)

## Introduction
Drawing custom shapes and animations in Flutter is made possible by the `CustomPainter` class, which allows you to define your own drawing logic. This class provides a `paint` method that is called whenever the widget needs to be painted on the screen. By overriding this method, you can create drawings and animations tailored to your specific needs.

## Drawing Shapes
Before we dive into animations, let's first understand how to draw shapes using the `CustomPainter` class. Here's an example of how to draw a simple circle:

```dart
class MyCustomPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()
      ..color = Colors.blue
      ..style = PaintingStyle.fill;

    final center = Offset(size.width / 2, size.height / 2);
    final radius = min(size.width, size.height) / 2;

    canvas.drawCircle(center, radius, paint);
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}
```

In this code snippet, we define a custom painter class `MyCustomPainter` that extends `CustomPainter`. The `paint` method is where we define the drawing logic. We initialize a `Paint` object with a blue color and set the style to fill. We then calculate the center and radius of the circle based on the size of the widget and use `canvas.drawCircle` to draw the circle on the canvas.

## Animating Drawings
To animate drawings in Flutter, we can use the `Animation` class along with the `AnimationController` class. Let's modify our previous example to animate the circle:

```dart
class MyCustomPainter extends CustomPainter with ChangeNotifier {
  late AnimationController _animationController;
  late Animation<double> _animation;

  MyCustomPainter() {
    _animationController = AnimationController(
      duration: const Duration(seconds: 1),
      vsync: this,
    );

    _animation = Tween(begin: 0.0, end: 1.0).animate(_animationController);
    _animationController.repeat(reverse: true);
  }

  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()
      ..color = Colors.blue.withOpacity(_animation.value)
      ..style = PaintingStyle.fill;

    final center = Offset(size.width / 2, size.height / 2);
    final radius = min(size.width, size.height) / 2;

    canvas.drawCircle(center, radius, paint);
    notifyListeners();
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}
```

In this modified code, we added an `_animationController` and an `_animation` object. We initialized the animation controller with a duration of 1 second and set it to repeat with reverse. We then created an opacity tween animation that goes from 0.0 to 1.0. Inside the `paint` method, we updated the circle's color by setting the opacity to the value of the animation. We also added a `notifyListeners` call to inform the widget that it needs to be repainted.

## Conclusion
Animating drawings in Flutter is made easy with the `CustomPainter` class. By combining it with the `Animation` and `AnimationController` classes, you can create captivating and interactive visual experiences. Whether you are creating games, visualizations, or user interfaces, Flutter provides a robust set of tools for animating drawings. So go ahead and unleash your creativity!

*Tags: #Flutter #Animations*
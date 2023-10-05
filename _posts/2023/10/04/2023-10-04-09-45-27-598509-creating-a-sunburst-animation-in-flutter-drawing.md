---
layout: post
title: "Creating a sunburst animation in Flutter drawing"
description: " "
date: 2023-10-04
tags: [setting]
comments: true
share: true
---

In this tutorial, we will explore how to create a sunburst animation using Flutter's drawing capabilities. A **sunburst** is a radial chart that divides a circle into multiple sections, representing different data categories. The sections are sized proportionally based on the values they represent, giving the illusion of a sun with rays.

## Table of Contents
- [Introduction](#introduction)
- [Setting up the Flutter Project](#setting-up-the-flutter-project)
- [Creating the Sunburst Widget](#creating-the-sunburst-widget)
- [Animating the Sunburst](#animating-the-sunburst)
- [Conclusion](#conclusion)

## Introduction

Flutter is a powerful open-source framework for building beautiful, native-looking applications for mobile, web, and desktop platforms. It provides various widgets and an easy-to-use drawing API that allows developers to create custom UI elements and animations.

## Setting up the Flutter Project

Before we begin, make sure you have Flutter installed on your system. If not, you can follow the [official Flutter installation guide](https://flutter.dev/docs/get-started/install) to get started.

Once Flutter is installed, create a new Flutter project using the following command:

```bash
flutter create sunburst_animation
```

Navigate into the project directory:

```bash
cd sunburst_animation
```

Open the project in your preferred code editor and let's get started!

## Creating the Sunburst Widget

In Flutter, we can use the `CustomPaint` widget to draw custom shapes on the screen. Let's create a new file called `sunburst_widget.dart` and define our `SunburstWidget` class as follows:

```dart
import 'package:flutter/material.dart';

class SunburstWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: SunburstPainter(),
    );
  }
}

class SunburstPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Implement sunburst drawing logic here
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}
```

In the `SunburstWidget` class, we use a `CustomPaint` widget and assign our custom `SunburstPainter` as the painter. Inside the `SunburstPainter` class, we will implement the actual drawing logic.

## Animating the Sunburst

To create an animation effect on our sunburst, we can utilize Flutter's built-in animation features. Let's modify the `SunburstWidget` class to include an animation controller:

```dart
class SunburstWidget extends StatefulWidget {
  @override
  _SunburstWidgetState createState() => _SunburstWidgetState();
}

class _SunburstWidgetState extends State<SunburstWidget>
    with SingleTickerProviderStateMixin {
  late final AnimationController _animationController;

  @override
  void initState() {
    super.initState();
    _animationController = AnimationController(
      duration: const Duration(seconds: 2),
      vsync: this,
    )..repeat(reverse: true);
  }

  @override
  void dispose() {
    _animationController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: SunburstPainter(
        animation: _animationController,
      ),
    );
  }
}
```

Here, we define a `AnimationController` that will control the animation of the sunburst. We set the duration to 2 seconds and set it to repeat in reverse. In the `build` method, we pass the animation controller to the `SunburstPainter` as an argument.

Now, let's make our sunburst drawing logic responsive to the animation. Modify the `SunburstPainter` class as follows:

```dart
class SunburstPainter extends CustomPainter {
  final Animation<double> animation;

  SunburstPainter({required this.animation}) : super(repaint: animation);

  @override
  void paint(Canvas canvas, Size size) {
    final radius = size.width / 2;
    final center = Offset(size.width / 2, size.height / 2);

    for (int i = 0; i < 6; i++) {
      final progress = i / 6.0;
      final startAngle = progress * 2 * pi;
      final sweepAngle = progress * 2 * pi * animation.value;

      final path = Path()
        ..moveTo(center.dx, center.dy)
        ..lineTo(radius * cos(startAngle), radius * sin(startAngle))
        ..arcTo(
          Rect.fromCircle(center: center, radius: radius),
          startAngle,
          sweepAngle,
          false,
        )
        ..lineTo(center.dx, center.dy)
        ..close();

      // Drawing the section
      canvas.drawPath(
        path,
        Paint()
          ..color = Colors.blue.withOpacity(0.5)
          ..style = PaintingStyle.fill,
      );
    }
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => true;
}
```

In this implementation, we iterate over six sections of the sunburst and calculate the starting and sweep angles based on the progress and animation value. We then draw each section by creating a closed path and filling it with a semi-transparent blue color.

## Conclusion

In this tutorial, we explored how to create a sunburst animation in Flutter's drawing capabilities. We learned how to utilize the `CustomPaint` widget to draw custom shapes and how to leverage Flutter's animation features to create interactive animations. Feel free to customize the sunburst design and experiment further with different animations to create stunning visual effects.

Remember to check the [Flutter documentation](https://flutter.dev/docs) for more information on custom painting and animations in Flutter.

Let's light up your app with a beautiful sunburst animation!

#flutter #animation
---
layout: post
title: "Creating water ripple effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

One of the powerful features of Flutter is the ability to create custom visual effects using shaders. In this tutorial, we're going to explore how to create a water ripple effect using SkiaShadersMask in Flutter. This effect can be used to enhance the visual appeal of your app or add a dynamic touch to your user interface.

## Prerequisites
Before we begin, make sure you have Flutter installed and set up on your machine. You should also have a basic understanding of Flutter and Dart programming language.

## Setting up the project
1. Create a new Flutter project using the command `flutter create water_ripple_effects`.
2. Open the project in your preferred code editor.

## Adding dependencies
In your project's `pubspec.yaml` file, add the following dependency:

```yaml
dependencies:
  skia: ^0.4.0
```

Then, run `flutter pub get` to download and add the dependency to your project.

## Implementing the water ripple effect
1. Create a new Dart file called `water_ripple_effects.dart` in the `lib` directory.
2. Add the following code to import the necessary packages and define a stateful widget:

```dart
import 'dart:ui';

import 'package:flutter/material.dart';
import 'package:skia/skia.dart';

class WaterRippleEffects extends StatefulWidget {
  @override
  _WaterRippleEffectsState createState() => _WaterRippleEffectsState();
}

class _WaterRippleEffectsState extends State<WaterRippleEffects> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Water Ripple Effects'),
      ),
      body: Center(
        child: CustomPaint(
          painter: WaterRipplePainter(),
        ),
      ),
    );
  }
}
```

3. Create a new Dart file called `water_ripple_painter.dart` in the same `lib` directory.
4. Add the following code to define a `WaterRipplePainter` class, which extends `CustomPainter`:

```dart
class WaterRipplePainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // TODO: Implement the water ripple effect logic
  }

  @override
  bool shouldRepaint(WaterRipplePainter oldDelegate) => true;
}
```

## Implementing the water ripple effect logic
1. Update the `paint` method in the `WaterRipplePainter` class with the following code:

```dart
void paint(Canvas canvas, Size size) {
  final paint = Paint()
    ..maskFilter = MaskFilter.blur(BlurStyle.normal, 10.0);
  
  final center = Offset(size.width / 2, size.height / 2);
  final radius = size.width / 3;
  
  final shader = SkiaShadersMask.createRadial(
    center,
    radius,
    [Colors.blue, Colors.transparent],
    TileMode.mirror,
  );
  
  final rect = Rect.fromCircle(center: center, radius: radius);
  
  canvas.saveLayer(
    rect,
    paint..shader = shader,
  );
  
  canvas.drawRect(
    Rect.fromLTWH(0, 0, size.width, size.height),
    Paint()
      ..shader = Gradient.linear(
        Offset(0, size.height / 2),
        Offset(size.width, size.height / 2),
        [Colors.blue, Colors.green],
      ),
  );
  
  canvas.restore();
}
```

2. Replace the `TODO` comment with the logic to create the water ripple effect. In this example, we use the `MaskFilter.blur` method to add a blur effect to the painting, and the `SkiaShadersMask.createRadial` method to create a radial gradient that gives the visual appearance of a ripple effect.

## Testing the water ripple effect
1. In the `main.dart` file, update the `void main` method to use the `WaterRippleEffects` widget:

```dart
void main() {
  runApp(MaterialApp(
    home: WaterRippleEffects(),
  ));
}
```

2. Run the app using `flutter run` command in your terminal or from your IDE.

Congratulations! You have successfully created a water ripple effect using SkiaShadersMask in Flutter. Feel free to experiment with different settings and properties to achieve the desired visual effect.
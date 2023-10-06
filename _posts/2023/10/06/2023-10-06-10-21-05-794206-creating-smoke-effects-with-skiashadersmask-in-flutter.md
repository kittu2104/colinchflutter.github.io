---
layout: post
title: "Creating smoke effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

## What is SkiaShadersMask?

SkiaShadersMask is a class provided by the Skia graphics library, which is used by Flutter for rendering. It allows you to apply various shader effects to your Flutter widgets, including the creation of smoke effects.

## Getting Started

Before we start creating smoke effects, make sure you have the latest version of Flutter installed on your machine. You can check the version by running the following command in your terminal:

```bash
flutter --version
```

If you don't have Flutter installed, please follow the Flutter installation guide provided by the Flutter team.

## Adding the Dependencies

To use SkiaShadersMask, we need to add the skia_flutter package to our Flutter project. Open your `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  skia_flutter: any
```

Save the file and run the following command in your terminal to fetch the package:

```bash
flutter pub get
```

Now that we have the package added, we can start creating smoke effects.

## Creating a Smoke Effect

To create a smoke effect, we'll use a combination of the SkiaPath and SkiaShadersMask classes. The SkiaPath class allows us to define the shape of our smoke, and the SkiaShadersMask class applies a shader effect to the defined shape.

Here's an example of how to create a smoke effect:

```dart
import 'package:flutter/material.dart';
import 'package:skia_flutter/skia_flutter.dart';

class SmokeEffect extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
      painter: _SmokePainter(),
    );
  }
}

class _SmokePainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()
      ..color = Colors.white.withOpacity(0.5)
      ..strokeWidth = 1
      ..style = PaintingStyle.fill;

    final path = Path();
    // Define your smoke shape using the path API
    path.moveTo(size.width * 0.25, size.height * 0.5);
    path.cubicTo(
        size.width * 0.2,
        size.height * 0.4,
        size.width * 0.4,
        size.height * 0.3,
        size.width * 0.5,
        size.height * 0.3,
    );
    // Add more path commands to complete your smoke shape

    final shader = LinearGradient(
      colors: [Colors.white.withOpacity(0.5), Colors.transparent],
      stops: [0, 1],
    ).createShader(path.getBounds());
    
    canvas.saveLayer(
      Offset.zero & size,
      Paint()..blendMode = BlendMode.dstIn,
    );
    canvas.drawPath(path, Paint()..shader = shader);
    canvas.restore();
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

In the above code, we define a `CustomPainter` called `_SmokePainter` that performs the actual painting of our smoke effect. We create a white paint with an opacity of 0.5 and a linear gradient shader that goes from white to transparent. We define a `Path` object and use the path API to create the shape of our smoke. Finally, we apply the shader to the path and draw it on the canvas.

To use the smoke effect, we create a `CustomPaint` widget, which takes an instance of `_SmokePainter` as its painter.

## Conclusion

In this tutorial, we explored how to create smoke effects using the SkiaShadersMask class in Flutter. We learned how to add the necessary dependencies, create a smoke effect using SkiaPath and SkiaShadersMask, and apply the effect to a Flutter widget.

Smoke effects can enhance the visual appeal of your Flutter application and bring life to your UI. Experiment with different shapes and colors to create unique smoke effects for your specific use case.

Make sure to check out the complete Skia documentation for more advanced shader effects and customization options.

Happy coding! #Flutter #SmokeEffects
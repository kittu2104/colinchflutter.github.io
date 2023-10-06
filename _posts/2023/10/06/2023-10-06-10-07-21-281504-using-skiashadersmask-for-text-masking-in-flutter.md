---
layout: post
title: "Using SkiaShadersMask for text masking in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Masking is a powerful technique that allows you to create stunning visual effects in your Flutter applications. It enables you to apply complex patterns or shapes to elements like text, images, or even containers. One way to achieve text masking in Flutter is by leveraging the Skia Shaders Mask.

In this article, we will explore how to use the Skia Shaders Mask to apply a mask to text in Flutter.

## Prerequisites
Before we proceed, make sure you have Flutter and Dart installed on your machine.

## Step 1: Set up a new Flutter project
First, create a new Flutter project using the following command:

```bash
flutter create text_masking_example
```

Navigate to the newly created project directory:

```bash
cd text_masking_example
```

## Step 2: Import the Skia package
To use Skia Shaders Mask in your Flutter project, you need to import the `flutter` package. Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  skia:
    path: /path/to/skia/package
```

Make sure to replace `/path/to/skia/package` with the correct path to the Skia package on your machine. Then, run the following command to install the dependencies:

```bash
flutter pub get
```

## Step 3: Implement the text masking
Open the `lib/main.dart` file and replace the default code with the following:

```dart
import 'dart:ui' as ui;

import 'package:flutter/material.dart';
import 'package:flutter/scheduler.dart';
import 'package:skia/skia.dart' as skia;

void main() {
  runApp(TextMaskingApp());
}

class TextMaskingApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: CustomPaint(
            size: Size(300, 300),
            painter: TextMaskingPainter(),
          ),
        ),
      ),
    );
  }
}

class TextMaskingPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final textSpan = TextSpan(
      text: 'Flutter',
      style: TextStyle(fontSize: 48, fontWeight: FontWeight.bold),
    );

    final textPainter = TextPainter(
      text: textSpan,
      textAlign: TextAlign.center,
      textDirection: TextDirection.ltr,
    );

    textPainter.layout(minWidth: 0, maxWidth: size.width);

    final textMask = skia.Paint()
      ..blendMode = skia.BlendMode.dstIn
      ..shader = _createTextMaskShader(size.width, size.height);

    canvas.saveLayer(null, Paint());
    SchedulerBinding.instance!.addPostFrameCallback((_) {
      canvas.clipRRect(RRect.fromRectAndRadius(
          Rect.fromLTWH(0, 0, size.width, size.height),
          Radius.circular(size.width / 2)));
    });

    canvas.drawRect(Rect.fromLTWH(0, 0, size.width, size.height), textMask);
    
    textPainter.paint(
        canvas, Offset((size.width - textPainter.width) / 2, 0));
    canvas.restore();
  }

  ui.Shader _createTextMaskShader(double width, double height) {
    final gradientColors = <Color>[
      Colors.transparent,
      Colors.white,
    ];

    final gradientStops = <double>[0.0, 1.0];

    return ui.Gradient.linear(
      Offset(width / 2, 0),
      Offset(width / 2, height),
      gradientColors,
      gradientStops,
      ui.TileMode.clamp,
    );
  }

  @override
  bool shouldRepaint(TextMaskingPainter oldDelegate) => false;
}
```

In the above code, we create a Flutter application with a custom `TextMaskingPainter` that extends `CustomPainter`. The `TextMaskingPainter` overrides the `paint` method to apply the text mask to the text.

Inside the `paint` method, we define the text span with the desired text and style. Then, we create a `TextPainter` to layout and paint the text. The text mask is defined as a `Paint` object with a `BlendMode.dstIn` blend mode and a text mask shader created using the `_createTextMaskShader` method.

Finally, we clip the canvas to a rounded rectangle shape and paint the text using the `textPainter`.

## Step 4: Run the app
Save the changes and run the Flutter app using the following command:

```bash
flutter run
```

You should see the text "Flutter" masked with a gradient effect. You can modify the text, style, or the mask shader to achieve different text masking effects.

## Conclusion
In this tutorial, we learned how to use the Skia Shaders Mask to create text masking in Flutter. By applying a custom mask shader, you can create visually appealing text effects to enhance the UI of your Flutter applications.
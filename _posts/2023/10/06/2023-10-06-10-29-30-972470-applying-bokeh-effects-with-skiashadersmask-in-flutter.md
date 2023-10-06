---
layout: post
title: "Applying bokeh effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Bokeh effects are a popular way to add a visually appealing blur to images in photography. In Flutter, you can apply bokeh effects to images using the SkiaShadersMask class from the `flutter_skia` package. SkiaShadersMask provides a simple and efficient way to create masks and apply them to images for bokeh effects.

In this tutorial, we will guide you through the process of applying bokeh effects to images using SkiaShadersMask in Flutter.

## Prerequisites

Before getting started, make sure you have Flutter and the `flutter_skia` package installed and set up in your development environment.

## Step 1: Add the `flutter_skia` Package to Your Project

Open your Flutter project in your preferred code editor. In your project's `pubspec.yaml` file, add the following dependency:

```yaml
dependencies:
  flutter_skia: ^0.0.5
```

Save the file, and run `flutter pub get` in the terminal to fetch and add the package to your project.

## Step 2: Import the Required Packages

In the Dart file where you want to apply the bokeh effect, import the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_skia/flutter_skia.dart';
```

## Step 3: Create a Custom Widget for the Bokeh Effect

To apply the bokeh effect to an image, you can create a custom widget that extends the `CustomPainter` class. This widget will override the `paint()` method and apply the bokeh effect using SkiaShadersMask.

Here's an example implementation of the custom widget:

```dart
class BokehEffectPainter extends CustomPainter {
  final ImageProvider imageProvider;

  BokehEffectPainter(this.imageProvider);

  @override
  void paint(Canvas canvas, Size size) async {
    final Image image = Image(image: await imageProvider.resolve(ImageConfiguration()));

    final Paint maskPaint = Paint();
    maskPaint.shader = SkiaShadersMask.bokeh(size.width, size.height, maskType: SkiaShadersMask.TYPE_APERTURE);

    final Rect rect = Offset.zero & size;
    canvas.drawImageRect(image, rect, rect, maskPaint);
  }

  @override
  bool shouldRepaint(BokehEffectPainter oldDelegate) {
    return oldDelegate.imageProvider != imageProvider;
  }
}
```

In the `paint()` method, the `SkiaShadersMask.bokeh()` function is used to create a bokeh mask with the specified size. The `maskType` parameter determines the type of bokeh effect you want to apply.

## Step 4: Display the Bokeh Effect Widget

To display the bokeh effect on an image, you can use the custom widget you created in the previous step in any Flutter widget tree.

Here's an example of how you can use the `BokehEffectPainter` widget:

```dart
class BokehEffectScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: CustomPaint(
          painter: BokehEffectPainter(NetworkImage('https://example.com/image.jpg')),
          child: Container(
            width: 300,
            height: 300,
            decoration: BoxDecoration(
              image: DecorationImage(
                image: NetworkImage('https://example.com/image.jpg'),
                fit: BoxFit.cover,
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

In this example, the `BokehEffectPainter` is used as the `painter` property of the `CustomPaint` widget. The `NetworkImage` is used as the image provider for the bokeh effect and the background image.

## Step 5: Run the App

Save your changes and run your Flutter app. You should see the bokeh effect applied to the specified image, creating a visually appealing blur effect.

## Conclusion

In this tutorial, you learned how to apply bokeh effects to images in Flutter using the SkiaShadersMask class from the `flutter_skia` package. Experiment with different mask types and sizes to create various bokeh effects and enhance the visual appeal of your Flutter apps.

#flutter #bokeh
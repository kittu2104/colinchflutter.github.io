---
layout: post
title: "Creating stencil effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Flutter provides a powerful 2D rendering engine called Skia, which allows you to create various visual effects. One such effect is the stencil effect, which allows you to apply a shape mask to your images or other graphical elements. In this blog post, we will explore how to create stencil effects using the `SkiaShadersMask` class in Flutter.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Creating the stencil mask](#creating-the-stencil-mask)
- [Applying the stencil effect](#applying-the-stencil-effect)
- [Conclusion](#conclusion)

## Prerequisites

To follow along with this tutorial, you need to have a basic understanding of Flutter and have Flutter SDK installed on your machine.

## Creating the stencil mask

To create a stencil mask, we need two components: the image or element we want to apply the effect to, and the shape mask that defines the visible areas. Let's start by creating the shape mask.

```dart
import 'package:flutter/material.dart';
import 'dart:ui' as ui;

class ShapeMask extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint();
    paint.color = Colors.black;
    paint.style = PaintingStyle.fill;

    final path = Path();
    // Define the shape of the mask using path commands
    path.moveTo(0, 0);
    path.lineTo(size.width, 0);
    path.lineTo(size.width / 2, size.height);
    path.close();

    // Apply the mask to the canvas
    canvas.drawPath(path, paint);
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return false;
  }
}

class StencilMaskPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SizedBox.expand(
        child: CustomPaint(
          painter: ShapeMask(),
          child: Image.asset('path_to_your_image.jpg', fit: BoxFit.cover),
        ),
      ),
    );
  }
}
```

In the above code, we create a custom painter class called `ShapeMask` that extends `CustomPainter`. Inside the `paint` method, we define the shape of the mask using `Path` commands. In this example, we create a triangular mask. You can modify the path commands to create different shapes.

Next, we define the paint properties like color and style. We then draw the shape onto the canvas using `drawPath`.

Inside the `StencilMaskPage` widget, we create a `CustomPaint` widget with the `ShapeMask` painter and an `Image` widget as its child. This ensures that the image is masked by the shape.

## Applying the stencil effect

Now that we have our stencil mask, let's apply it to our image to create the stencil effect.

```dart
import 'package:flutter/material.dart';
import 'dart:ui' as ui;

class StencilShader extends StatelessWidget {
  final ImageProvider image;
  final CustomPainter mask;

  const StencilShader({required this.image, required this.mask});

  @override
  Widget build(BuildContext context) {
    return ShaderMask(
      shaderCallback: (Rect bounds) {
        return ui.ImageShader(
          // Convert the widget image to a raw image
          image as ui.Image,
          TileMode.clamp,
          TileMode.clamp,
          Float64List.fromList(Matrix4.identity().storage),
        );
      },
      blendMode: BlendMode.dstIn,
      child: CustomPaint(
        painter: mask,
        child: Image(image: image, fit: BoxFit.cover),
      ),
    );
  }
}

class StencilEffectPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SizedBox.expand(
        child: StencilShader(
          image: AssetImage('path_to_your_image.jpg'),
          mask: ShapeMask(),
        ),
      ),
    );
  }
}
```

In the above code, we create a `StencilShader` widget that takes the image and mask as parameters. Inside the `ShaderMask` widget, we use the `ui.ImageShader` class to create a shader object with the image as the input. We set the `blendMode` to `BlendMode.dstIn`. This mode ensures that only the areas defined by the mask are visible.

Finally, we wrap our custom painter widget with the `StencilShader` widget in the `StencilEffectPage` widget.

## Conclusion

In this blog post, we explored how to create stencil effects using the `SkiaShadersMask` class in Flutter. We learned how to create a shape mask using a custom painter, and then apply the stencil effect using the `ShaderMask` widget. With these techniques, you can create interesting visual effects in your Flutter applications.

#flutter #skia
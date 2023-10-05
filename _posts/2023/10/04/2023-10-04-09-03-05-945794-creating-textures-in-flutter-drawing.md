---
layout: post
title: "Creating textures in Flutter drawing"
description: " "
date: 2023-10-04
tags: [using]
comments: true
share: true
---

Textures can add depth and visual appeal to your Flutter app's user interface. By combining different hues, patterns, and textures, you can create visually rich and dynamic UI elements. Flutter provides the `CustomPaint` widget which allows you to draw custom graphics using the `Canvas` and `Paint` classes. In this article, we will explore how to create textures in Flutter drawing.

## Table of Contents
- [Introduction](#introduction)
- [Using the CustomPaint Widget](#using-the-custompaint-widget)
- [Creating a Texture](#creating-a-texture)
- [Applying Texture to a Shape](#applying-texture-to-a-shape)
- [Conclusion](#conclusion)

## Introduction

Texturing involves applying a repeating pattern or image to a shape, giving it a textured appearance. In Flutter, we can achieve this by using the `Shader` class from the `dart:ui` library. A `Shader` defines the pattern to be applied to a shape during rendering.

## Using the CustomPaint Widget

To draw custom graphics in Flutter, we can use the `CustomPaint` widget. This widget provides a `painter` property to define the custom painting logic. The `CustomPainter` class allows us to override the `paint` method, where we can use the `Canvas` object to draw our custom graphics.

## Creating a Texture

To create a texture in Flutter drawing, we need to create a `Shader` object. The `Shader` class provides various options for creating textures, including:

- **RadialGradient**: This allows us to create a gradient that radiates outward from a center point.
- **LinearGradient**: This creates a gradient that transitions between two colors in a linear direction.
- **ImageShader**: This applies an image as a texture to a shape.

Let's take a look at an example of creating a linear gradient texture using the `LinearGradient` class:

```dart
final shader = LinearGradient(
  colors: [Colors.blue, Colors.green],
).createShader(Rect.fromLTWH(0.0, 0.0, 200.0, 200.0));
```

In the above example, we create a linear gradient shader that transitions from blue to green. We then specify the dimensions of the shape to be textured using the `Rect.fromLTWH` method.

## Applying Texture to a Shape

Once we have created the texture using a `Shader` object, we can apply it to a shape while painting. Inside the `paint` method of our `CustomPainter`, we can set the `shader` property of the `Paint` object to apply the texture to the desired shape.

```dart
@override
void paint(Canvas canvas, Size size) {
  final paint = Paint()
    ..shader = shader;

  // Draw the textured shape
  canvas.drawRect(Rect.fromLTWH(0.0, 0.0, size.width, size.height), paint);
}
```

In the above example, we set the `shader` property of the `Paint` object to the previously created linear gradient shader. We then draw a rectangle using the `canvas.drawRect` method, passing the desired dimensions and the `paint` object.

## Conclusion

With the `CustomPaint` widget and the `Shader` class, you can create textures in Flutter drawing to enhance the visual appeal of your app's UI. Experiment with different shaders and shapes to create unique and engaging textures. Texture can be a powerful tool to transform your app's user experience. Happy drawing!

## #flutter #texturing
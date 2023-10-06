---
layout: post
title: "Applying ASCII art effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

ASCII art is a technique that uses a combination of characters and symbols to create images and visual effects. It has been widely used in computer graphics since the early days of computing. In this article, we will explore how to apply ASCII art effects to images using SkiaShadersMask in Flutter.

## Table of Contents
- [What is SkiaShadersMask?](#what-is-skiashadersmask)
- [Creating ASCII Art Effects](#creating-ascii-art-effects)
- [Applying SkiaShadersMask](#applying-skiashadersmask)
- [Conclusion](#conclusion)

## What is SkiaShadersMask?

SkiaShadersMask is a feature in the Skia library, which is the graphics engine used by Flutter. It allows developers to create custom masks that can be applied to images or other graphical elements. By using SkiaShadersMask, we can create complex and artistic effects by manipulating the visual appearance of the masked area.

## Creating ASCII Art Effects

Before we can apply the ASCII art effects, we need to convert our images into ASCII representation. There are various libraries and techniques available for this purpose. One popular library is `ascii_art` which can be imported into your Flutter project.

```dart
import 'package:ascii_art/ascii_art.dart';

void main() {
  final image = Image(image: AssetImage('path_to_image.png'));
  final ascii = AsciiArt(image.width, image.height, fontHeight: 4);
  final art = ascii.fromImage(image);
  print(art);
}
```

In the code snippet above, we import the `ascii_art` library, load an image, and create an instance of `AsciiArt`. We then print the converted ASCII art by calling the `fromImage` method.

## Applying SkiaShadersMask

To apply the ASCII art mask using SkiaShadersMask, we first need to define a custom `Shader` that represents the ASCII pattern. We can then create a `ShaderMask` widget and set the `shader` property to the custom shader.

```dart
import 'dart:ui' as ui;

final asciiPattern = "ASCII_ART_PATTERN";

final asciiShader = ui.Shader((bounds) {
  final path = ui.Path();
  final style = ui.TextStyle(
    fontFamily: 'monospace',
    fontSize: 10,
  );

  final paragraphBuilder = ui.ParagraphBuilder(ui.ParagraphStyle(
    textStyle: style,
  ));
  paragraphBuilder.addText(asciiPattern);

  final constraints = ui.ParagraphConstraints(width: bounds.width);
  final paragraph = paragraphBuilder.build();
  paragraph.layout(constraints);

  path.addRect(bounds);
  path.addPath(
    paragraph.getPaths(ui.Point(0, 0)),
    Offset.zero,
  );
  
  return path.createShader(ui.Rect.fromLTRB(bounds.left, bounds.top, bounds.right, bounds.bottom));
});

Widget build(BuildContext context) {
  return ShaderMask(
    shaderCallback: (bounds) => asciiShader,
    child: Image(image: AssetImage('path_to_image.png')),
  );
}
```

In the code snippet above, we define the `asciiPattern` which represents the ASCII art pattern generated earlier. We create a custom `Shader` using the `ui.Shader` constructor and define the path using the ASCII pattern. The `ui.Paragraph` class is used to create the path for the ASCII pattern.

Finally, we can use the `ShaderMask` widget to apply the mask to an `Image` widget. The `shaderCallback` property of `ShaderMask` allows us to define the custom shader that we created earlier.

## Conclusion

In this article, we explored how to apply ASCII art effects to images using SkiaShadersMask in Flutter. By converting images into ASCII representation and creating a custom shader, we can achieve unique and artistic visual effects. Feel free to experiment with different ASCII patterns and explore the possibilities of SkiaShadersMask in your Flutter projects.

#flutter #ASCIIart
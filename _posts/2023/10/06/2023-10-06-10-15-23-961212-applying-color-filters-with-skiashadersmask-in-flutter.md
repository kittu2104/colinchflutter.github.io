---
layout: post
title: "Applying color filters with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Color filters are a powerful tool for applying effects to images or altering the colors of UI elements in Flutter. One way to apply color filters is by using the SkiaShadersMask class, which allows you to create customized color filter effects.

Skia is an open-source 2D graphics library that Flutter uses to render visuals. SkiaShadersMask is a class provided by Skia that allows you to create complex shader-based color filter effects.

## Getting started

To get started, make sure you have Flutter installed on your machine. You can install Flutter from the official Flutter website.

## Adding the dependency

First, you need to add the `skia` package as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  skia:
```

Then, run `flutter pub get` to download and install the package.

## Applying a color filter with SkiaShadersMask

To apply a color filter using SkiaShadersMask, you need to create a custom `ShaderMask` widget that uses the SkiaShadersMask class.

Here's an example:

```dart
import 'package:flutter/material.dart';
import 'package:skia/skia.dart' as skia;

class ColorFilterExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ShaderMask(
      shaderCallback: (Rect bounds) {
        return skia.SkiaShadersMask(
          skia.Paint()
            ..colorFilter = skia.ColorFilter.mode(
              const skia.Color.fromARGB(128, 255, 0, 0),
              skia.BlendMode.srcIn,
            ),
          bounds: bounds,
        );
      },
      child: Image.network('https://example.com/image.jpg'),
    );
  }
}
```

In the `shaderCallback` of the `ShaderMask`, we create an instance of `skia.SkiaShadersMask`, passing a `Paint` instance with the desired color filter effect.

In this example, we are applying a red color filter with 50% opacity (`fromARGB(128, 255, 0, 0)`) using the `srcIn` blend mode. You can customize the color filter and blend mode according to your needs.

The `bounds` parameter is used to specify the size and position of the shader. In this example, we pass the `bounds` parameter as the bounds of the `ShaderMask` widget itself.

Finally, we wrap the image or UI element that we want to apply the color filter to, in this case an `Image.network` widget.

## Conclusion

Color filters can add visual flair and enhance the design of your Flutter applications. With the SkiaShadersMask class, you have the flexibility to create custom color filter effects using the power of Skia shaders.

Experiment with different color filters and blend modes to create unique effects that suit your app's design aesthetics.
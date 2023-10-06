---
layout: post
title: "Applying blur effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In Flutter, you can use various techniques to apply blur effects to your UI components. One powerful way to achieve this is by using the `SkiaShadersMask` class provided by the flutter_svg package. This allows you to create custom blur masks using shaders provided by the Skia graphics library.

## What is SkiaShadersMask?

`SkiaShadersMask` is a class that allows you to apply custom shaders as masks in Flutter. Shaders are programs that run on the graphics hardware and define how colors and patterns are rendered. By using shaders as masks, you can control how UI components are blurred, giving you more flexibility and control over the blur effect.

## Adding the flutter_svg package

To use the `SkiaShadersMask` class, you need to add the `flutter_svg` package to your Flutter project. Open your project's `pubspec.yaml` file and add the following line under `dependencies`:

```yaml
dependencies:
  flutter_svg: ^0.22.0
```

After adding the dependency, run `flutter pub get` to fetch the package.

## Applying the blur effect

Once you have added the `flutter_svg` package to your project, you can apply the blur effect using the `SkiaShadersMask` class.

First, import the necessary packages in your Dart file:

```dart
import 'package:flutter_svg/flutter_svg.dart';
import 'package:flutter_svg/svg.dart';
```

Then, create an instance of `SkiaShadersMask` and pass the desired shader to apply the blur effect:

```dart
SkiaShadersMask mask = SkiaShadersMask(
  shader: ImageShader(
    svgRoot, // The root <svg> element containing the component to blur
    TileMode.clamp, // Specify how to tile the image
    TileMode.clamp, // Specify how to tile the image
    Float64List.fromList(<double>[0, 0, 0, 1]), // Transformation matrix
  ),
);
```

Finally, apply the `SkiaShadersMask` as a mask to the desired widget using the `ShaderMask` class:

```dart
ShaderMask(
  blendMode: BlendMode.srcATop,
  shaderCallback: (Rect bounds) => mask.shader!,
  child: YourComponent(),
)
```

Make sure to replace `YourComponent()` with the widget you want to apply the blur effect to.

## Conclusion

By using the `SkiaShadersMask` class, you can easily apply blur effects to your Flutter UI components. This provides you with more control and flexibility over the appearance of your app. Experiment with different shaders and settings to achieve the desired blur effect for your project.

#flutter #blur-effect
---
layout: post
title: "Using SkiaShadersMask for creating video filters in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this article, we will explore how to use the SkiaShadersMask package in Flutter to create video filters. SkiaShadersMask is a powerful library that allows us to apply various shader effects, such as masks and gradients, to our videos in real-time.

## Table of Contents

- [What is SkiaShadersMask?](#what-is-skiashadersmask)
- [Installing the SkiaShadersMask Package](#installing-the-skiashadersmask-package)
- [Creating a Video Filter](#creating-a-video-filter)
- [Applying the Video Filter](#applying-the-video-filter)
- [Conclusion](#conclusion)
- [Resources](#resources)

## What is SkiaShadersMask?

SkiaShadersMask is a Flutter package that provides a set of shader effects for creating video filters. It uses the Skia library, a powerful 2D graphics API, to render the shaders on the screen. With SkiaShadersMask, you can easily apply various effects like masks, gradients, and blend modes to your videos.

## Installing the SkiaShadersMask Package

To use SkiaShadersMask in your Flutter project, you need to add it as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  skiashadersmask: ^1.0.0
```

Then, you can run `flutter pub get` to install the package.

## Creating a Video Filter

To create a video filter, we need to define a custom `Shader` using SkiaShadersMask. Let's start by creating a new file called `video_filter.dart` and importing the necessary packages:

```dart
import 'package:flutter/widgets.dart';
import 'package:skiashadersmask/skiashadersmask.dart';
```

Next, we can create a new class called `VideoFilter` that extends `Shader`:

```dart
class VideoFilter extends Shader {
  @override
  ShaderContext context;

  VideoFilter(this.context);
}
```

Inside the `VideoFilter` class, we need to implement the abstract methods from the `Shader` class, such as `createShader` and `updateShader`. These methods define how the shader will be rendered on the screen. 

For example, to create a simple Grayscale filter, we can override the `createShader` method as follows:

```dart
@override
SkShader createShader(Rect rect) {
  final imageHeight = context.image.height;
  final imageWidth = context.image.width;

  return SkShaderMask(
    shader: SkShaderImage(imageWidth, imageHeight, context.textures[0]), // Use the first texture as input
    mask: SkMaskFilterGrayscale(),
  );
}
```

In this example, we create a `SkShaderMask` with the `SkShaderImage` as the input texture and apply the `SkMaskFilterGrayscale` to convert the colors to grayscale.

## Applying the Video Filter

Once we have our custom `VideoFilter` defined, we can apply it to a video using the `ShaderMask` widget in Flutter. Here's an example of how to use it:

```dart
ShaderMask(
  blendMode: BlendMode.overlay, // Optional blend mode
  shaderCallback: (Rect bounds) {
    final videoFilter = VideoFilter(ShaderContext(context));
    return videoFilter;
  },
  child: VideoPlayer(), // Your video widget here
)
```

In this example, we use the `ShaderMask` widget and provide the `VideoFilter` shader as the `shaderCallback`. You can also specify an optional blend mode to modify how the shader is blended with the underlying video.

## Conclusion

SkiaShadersMask is a powerful package for creating video filters in Flutter. By using custom shaders and the `ShaderMask` widget, you can easily apply various effects to your videos in real-time. Experiment with different shaders and parameters to create unique and stunning visual effects.

## Resources

- [SkiaShadersMask GitHub Repository](https://github.com/fluttercandies/flutter.skia_shaders_mask)
- [Skia Library Documentation](https://flutter.github.io/skia/)
- [Flutter Documentation](https://flutter.dev/docs)

#flutter #flutterdevelopment
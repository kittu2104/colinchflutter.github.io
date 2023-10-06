---
layout: post
title: "How to apply image masks with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In Flutter, you can apply image masks using the `SkiaShadersMask` class from the `flutter_svg` package. This allows you to create interesting visual effects by combining images and custom masks.

## Table of Contents
- [Setting up the Environment](#setting-up-the-environment)
- [Applying Image Masks](#applying-image-masks)
- [Creating a Custom Mask](#creating-a-custom-mask)
- [Conclusion](#conclusion)

## Setting up the Environment

To get started, make sure you have the `flutter_svg` package added to your Flutter project. You can add it to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_svg: ^0.22.0
```

Run `flutter pub get` to fetch the package.

## Applying Image Masks

Once you have `flutter_svg` added to your project, you can use the `SkiaShadersMask` class to apply image masks. Here's an example of applying a mask to an image:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';

class MaskedImage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ShaderMask(
      shaderCallback: (Rect bounds) {
        return SkiaShadersMask(
          SvgPicture.asset(
            'assets/mask.svg',
          ),
        ).createShader(bounds);
      },
      child: Image.asset('assets/image.png'),
    );
  }
}
```

In the example above, we use `ShaderMask` widget to apply the `SkiaShadersMask` using the `shaderCallback` parameter. The `SkiaShadersMask` takes an `SvgPicture` as the mask and creates a shader using the `createShader` method. Finally, we wrap the `Image.asset` widget with the `ShaderMask` to apply the mask.

## Creating a Custom Mask

To create a custom mask, you can use an SVG file. SVG stands for Scalable Vector Graphics and is a powerful way to define vector-based images. You can create an SVG file using software like Adobe Illustrator or Inkscape.

Here's an example of a simple SVG file that can be used as a mask:

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100">
  <circle cx="50" cy="50" r="40" />
</svg>
```

Save this SVG file as `mask.svg` in your assets folder.

## Conclusion

By using the `SkiaShadersMask` class from the `flutter_svg` package, you can easily apply image masks in Flutter. This allows you to create dynamic and visually appealing effects in your app. Experiment with different masks and combine them with images to create unique visual experiences.

#flutter #flutter_svg
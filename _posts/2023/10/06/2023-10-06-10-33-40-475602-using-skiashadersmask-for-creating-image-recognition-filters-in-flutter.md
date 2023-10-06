---
layout: post
title: "Using SkiaShadersMask for creating image recognition filters in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Image recognition filters can add an exciting interactive experience to your Flutter app. With the help of the SkiaShadersMask package, you can easily implement image recognition filters to identify objects in a user's images.

SkiaShadersMask is a Flutter plugin that allows you to leverage the power of Skia graphics library to create custom image filters. This package provides a variety of built-in shaders that can be used to apply filters such as blurs, gradients, and color manipulations to images.

To get started, follow these steps:

## Step 1: Add the SkiaShadersMask package to your pubspec.yaml file

Add the following line to your pubspec.yaml file under the `dependencies` section:

```dart
dependencies:
  skia_shaders_mask: ^1.0.0
```

Save the file and run `flutter pub get` to download the package.

## Step 2: Import the SkiaShadersMask package

In your Dart file, import the SkiaShadersMask package:

```dart
import 'package:skia_shaders_mask/skia_shaders_mask.dart';
```

## Step 3: Create an Image filter

To create an image filter, start by importing the necessary classes:

```dart
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';
import 'package:path_provider/path_provider.dart';
import 'package:skia_shaders_mask/skia_shaders_mask.dart';
```

Then, create an instance of `SkiaShadersMask` and apply the desired filters:

```dart
SkiaShadersMask _mask;

Future<void> loadImageWithMask() async {
  final ImagePicker _picker = ImagePicker();
  final PickedFile pickedImage = await _picker.getImage(source: ImageSource.gallery);
  final imageBytes = await pickedImage.readAsBytes();
  final tempDir = await getTemporaryDirectory();

  final maskPath = '${tempDir.path}/mask.png';
  await _mask.makeMask(imageBytes, maskPath);

  setState(() {
    _mask = SkiaShadersMask(maskPath: maskPath);
  });
}
```

In the example above, we use the `ImagePicker` package to allow the user to select an image from the gallery. Then, we use the `makeMask` method from the `SkiaShadersMask` class to create a binary mask image from the selected image. Finally, we pass the generated mask image path to the `SkiaShadersMask` constructor to create an instance of the mask.

## Step 4: Apply the filter to an image widget

To apply the created filter to an image widget, wrap the image widget with a `ShaderMask` widget and pass the mask instance as the `shaderCallback` parameter:

```dart
ShaderMask(
  shaderCallback: (Rect bounds) {
    return _mask.shader;
  },
  blendMode: BlendMode.srcATop,
  child: Image.network('https://example.com/image.jpg'),
),
```

In this example, we use the `Image.network` widget to display an image from a URL. We wrap it with a `ShaderMask` widget and pass the mask's `shader` as the `shaderCallback` parameter.

## Conclusion

By using the SkiaShadersMask package, you can easily create image recognition filters in your Flutter app. Experiment with different filters and effects to provide an engaging visual experience for your users.

Remember to expand your knowledge further by exploring the SkiaShadersMask documentation and experimenting with the package's capabilities.

#flutter #imageprocessing
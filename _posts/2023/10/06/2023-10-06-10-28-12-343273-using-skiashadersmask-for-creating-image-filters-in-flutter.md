---
layout: post
title: "Using SkiaShadersMask for creating image filters in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to use the SkiaShadersMask library in Flutter to create stunning image filters. The SkiaShadersMask library is a powerful tool that allows us to apply custom effects to images by manipulating the pixels using shaders.

## Prerequisites

Before you start, make sure you have the following:

- Flutter SDK installed on your machine
- A basic understanding of Flutter concepts

## Step 1: Add the dependency

To use the SkiaShadersMask library, we need to add it as a dependency in our `pubspec.yaml` file. Open the file and add the following lines under the `dependencies` section:

```yaml
dependencies:
  flutter:
    sdk: flutter
  skia_shaders_mask: ^1.0.0
```

Then, run `flutter pub get` to fetch the package.

## Step 2: Import the library

Open the Dart file where you want to apply the image filter and import the SkiaShadersMask library:

```dart
import 'package:skia_shaders_mask/skia_shaders_mask.dart';
```

## Step 3: Create an image filter

Next, let's create a basic image filter using the SkiaShadersMask library. In this example, we will apply a grayscale effect to an image. Add the following code to your Dart file:

```dart
import 'dart:typed_data';

import 'package:flutter/material.dart';
import 'package:image/image.dart' as img;
import 'package:skia_shaders_mask/skia_shaders_mask.dart';

Future<Uint8List> applyGrayscaleFilter(String imagePath) async {
  final imageBytes = await rootBundle.load(imagePath);
  final image = img.decodeImage(imageBytes.buffer.asUint8List())!;
  final filter = SkiaShadersMask.fromImage(image).grayscale();
  final filteredImage = filter.apply(image);
  return img.encodeJpg(filteredImage);
}
```

In this code snippet, we load the image using the `rootBundle` from the Flutter framework and convert it to an `Image` object using the `image` library. Then, we create a `SkiaShadersMask` object from the image and apply the `grayscale` filter to it. Finally, we encode the filtered image as a JPEG and return the resulting bytes.

## Step 4: Display the filtered image

To display the filtered image in your Flutter app, use the following code:

```dart
class FilteredImage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return FutureBuilder<Uint8List>(
      future: applyGrayscaleFilter('path_to_your_image'),
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.done &&
            snapshot.hasData) {
          return Image.memory(snapshot.data);
        } else {
          return CircularProgressIndicator();
        }
      },
    );
  }
}
```

Replace `'path_to_your_image'` with the actual path to your image file.

## Conclusion

By using the SkiaShadersMask library, we can easily create customized image filters in Flutter. You can explore other available filters and effects provided by the library to enhance your app's visual appeal. Don't forget to experiment with different image manipulation techniques and unleash your creativity!

#flutter #imagefilter
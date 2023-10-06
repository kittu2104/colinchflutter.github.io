---
layout: post
title: "Applying image overlays with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In Flutter, you can apply image overlays using the `SkiaShadersMask` class, which provides a powerful way to blend and mask images together. This technique is commonly used to create effects such as adding textures or patterns to images or applying filters to change their appearance.

## Setting up the project

Before we dive into applying image overlays, let's set up a Flutter project. Follow these steps:

1. Open your terminal or command prompt.
2. Create a new Flutter project using the `flutter create` command:

```bash
flutter create image_overlay_project
```

3. Change to the project directory:

```bash
cd image_overlay_project
```

4. Open the project in your preferred code editor.

Now that the project is set up, we can start working on applying image overlays.

## Applying image overlay

1. First, add an image file to your project. You can use any image you prefer. Save it in the `assets` folder of your Flutter project. For example, let's assume the image is named `overlay_image.png`.

2. Open the `pubspec.yaml` file in your project directory and add the following line under the `flutter` section:

```yaml
assets:
  - assets/overlay_image.png
```

This step ensures that the image is available to your Flutter application.

3. Open the main.dart file and import the required packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'dart:ui' as ui;
```

4. Create a method to load the overlay image using the `rootBundle`:

```dart
Future<ui.Image> loadImage() async {
  final ByteData data = await rootBundle.load('assets/overlay_image.png');
  final Completer<ui.Image> completer = Completer();

  ui.decodeImageFromList(data.buffer.asUint8List(), (ui.Image img) {
    return completer.complete(img);
  });

  return completer.future;
}
```

5. In the `build` method of the main `MyApp` widget, call the `loadImage` method and use the result to create a `SkiaShadersMask` widget:

```dart
Widget build(BuildContext context) {
  return FutureBuilder(
    future: loadImage(),
    builder: (BuildContext context, AsyncSnapshot<ui.Image> snapshot) {
      if (snapshot.connectionState == ConnectionState.done) {
        final ui.Image overlayImage = snapshot.data;
        return SkiaShadersMask(
          blendMode: BlendMode.multiply,
          colors: [Colors.black, Colors.transparent],
          shaderCallbacks: [
            (Rect bounds) {
              final tileMode = TileMode.mirror;

              final shaderRect = Rect.fromLTWH(
                0,
                0,
                overlayImage.width.toDouble(),
                overlayImage.height.toDouble(),
              );

              final paint = Paint()
                ..shader = ImageShader(
                  overlayImage,
                  tileMode,
                  tileMode,
                  Float64List.fromList([
                    1, 0, 0, 0, // R
                    0, 1, 0, 0, // G
                    0, 0, 1, 0, // B
                    0, 0, 0, 0, // A
                  ]),
                );

              return paint.createShader(shaderRect);
            },
          ],
          child: YourWidget(),
        );
      } else {
        return CircularProgressIndicator();
      }
    },
  );
}
```

In this example, we create a `SkiaShadersMask` widget and provide the overlay image as a shader. The `blendMode` determines how the overlay blends with the underlying image. In this case, we are using `BlendMode.multiply` to create a color multiplication effect. The `colors` parameter defines the colors to apply to each channel of the shader (R, G, B, A).

6. Replace `YourWidget` with the widget you want to apply the image overlay to. For example, if you want to apply the overlay to an `Image` widget, replace `YourWidget` with `Image.network('https://example.com/image.jpg')`.

And that's it! You've applied an image overlay using the `SkiaShadersMask` class in Flutter.

## Conclusion

Using the `SkiaShadersMask` class in Flutter allows you to easily apply image overlays and create a variety of visually appealing effects. Experiment with different blend modes and colors to achieve the desired result. Happy coding!

#flutter #imageoverlay
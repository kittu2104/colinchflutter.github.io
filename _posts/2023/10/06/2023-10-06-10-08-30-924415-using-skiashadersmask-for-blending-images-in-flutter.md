---
layout: post
title: "Using SkiaShadersMask for blending images in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

When it comes to image blending in Flutter, the `SkiaShader` class offers a powerful solution. One of the most useful subclasses of `SkiaShader` is `SkiaShadersMask`, which allows for advanced blending effects using masks. In this blog post, we will explore how to use `SkiaShadersMask` for blending images in Flutter.

## What is SkiaShadersMask?

`SkiaShadersMask` is a class in the [Flutter Skia](https://github.com/flutter/engine/tree/master/src/sksl) library that provides a way to apply complex blending effects to images. It allows you to define a mask using a bitmap, and then use that mask to blend two images together in various ways.

## Setting up the Project

To get started, create a new Flutter project by running the following commands in your terminal:

```bash
flutter create image_blend_example
cd image_blend_example
```

Open the project in your preferred code editor and add the following dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  skia:
    git:
      url: git://github.com/flutter/engine.git
      path: third_party/skia
```

Save the file and run `flutter pub get` to fetch the dependencies.

## Blending Images with SkiaShadersMask

Once you have set up the project, you can start using `SkiaShadersMask` to blend images. Here is an example of how to blend two images together:

```dart
import 'package:flutter/material.dart';
import 'package:skia/skia.dart';

class ImageBlendPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final Image image1 = Image.asset('assets/image1.png');
    final Image image2 = Image.asset('assets/image2.png');

    final PictureRecorder recorder = PictureRecorder();
    final Canvas canvas = Canvas(recorder);

    final Rect rect1 = Rect.fromLTRB(0, 0, 200, 200);
    final Rect rect2 = Rect.fromLTRB(100, 100, 300, 300);

    final Paint paint = Paint();
    final MaskFilter maskFilter = MaskFilter.blur(BlurStyle.solid, 10);

    final Shader shader = SkiaShadersMask(
      rect1,
      rect2,
      image1.path,
      image2.path,
      paint,
      maskFilter,
    );

    paint.shader = shader;
    canvas.drawRect(Rect.fromLTRB(0, 0, 400, 400), paint);

    final Picture picture = recorder.endRecording();
    final PictureImage pictureImage = PictureImage(picture);

    return Scaffold(
      body: Center(
        child: Image(image: pictureImage),
      ),
    );
  }
}
```

In this example, we create two `Image` widgets representing the images we want to blend. Then, we create a `PictureRecorder` and a `Canvas` to draw on. We define the rectangles for positioning the images and set up a `Paint` object with a `MaskFilter` for applying the blending effect.

Next, we create a `SkiaShadersMask` shader passing in the rectangular regions, image paths, paint, and mask filter. We set the shader to the paint object and draw a rectangle on the canvas. Finally, we convert the recorded `Picture` to a `PictureImage` and display it using the `Image` widget.

Make sure to replace `'assets/image1.png'` and `'assets/image2.png'` with the actual paths to your images.

## Conclusion

With the help of `SkiaShadersMask`, you can easily blend images in Flutter and achieve stunning visual effects. Experiment with different mask shapes, images, and blending modes to create unique and eye-catching designs.

Remember to import the necessary packages and keep your Skia version up to date for optimal performance. For more information about SkiaShadersMask and the Flutter Skia library, refer to the [official documentation](https://api.flutter.dev/flutter/skia/SkiaShadersMask-class.html).

Happy blending! 🎨

#flutter #imageblending
---
layout: post
title: "Applying light painting effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In the world of Flutter, we can apply light painting effects to our app's UI using the SkiaShadersMask widget. SkiaShadersMask is a powerful tool that allows us to mask our UI components with custom shaders, giving us the ability to create stunning visual effects.

In this tutorial, we'll walk through the steps of applying a light painting effect with SkiaShadersMask in Flutter.

## Prerequisites

Before we begin, make sure you have Flutter installed on your machine. You can download Flutter from the official Flutter website.

## Setting up the project

Create a new Flutter project using the following command:

```dart
flutter create light_painting_app
```

Navigate into the project directory:

```dart
cd light_painting_app
```

## Adding dependencies

We'll need to add the `flutter_svg` package to our project, as it provides support for rendering SVG images. Open the `pubspec.yaml` file and add the following line under `dependencies`:

```yaml
dependencies:
  flutter_svg: ^1.0.0
```

Save the file and run the following command to fetch the dependencies:

```dart
flutter pub get
```

## Implementing the light painting effect

1. Create a new file called `light_painting.dart` in the `lib` directory.

2. Import the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';
import 'package:skia_shaders_mask/skia_shaders_mask.dart';
```

3. Create a new `StatelessWidget` called `LightPaintingEffect`:

```dart
class LightPaintingEffect extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Light Painting Effect'),
      ),
      body: Center(
        child: SkiaShadersMask(
          child: SvgPicture.asset(
            'assets/light_painting.svg',
            width: 300,
            height: 300,
          ),
          shader: LinearGradient(
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
            colors: [
              Colors.transparent,
              Colors.blue.withOpacity(0.5),
              Colors.transparent,
            ],
          ).createShader(Rect.fromLTRB(0, 0, 300, 300)),
        ),
      ),
    );
  }
}
```

In this code snippet, we've created a basic layout with an `AppBar` and a `Center` widget. Inside the `Center` widget, we've added the `SkiaShadersMask` widget, which takes two parameters: a child widget (in this case, an SVG image) and a shader.

4. Add the SVG asset to the project:

   - Create a new directory called `assets` in the root of your project.
   - Place an SVG image (e.g., `light_painting.svg`) inside the `assets` directory.

5. Register the SVG asset in the `pubspec.yaml` file:

```yaml
flutter:
  assets:
    - assets/
```

6. Run the app and see the light painting effect in action:

```dart
void main() {
  runApp(MaterialApp(
    home: LightPaintingEffect(),
  ));
}
```

By following these steps, you should now see the light painting effect rendered on your Flutter app's screen.

## Conclusion

In this tutorial, we explored how to apply a light painting effect using SkiaShadersMask in Flutter. By leveraging the power of SkiaShadersMask and the `flutter_svg` package, we were able to create an immersive and visually stunning UI effect.

Don't be afraid to experiment with different shaders and SVG images to create unique and captivating experiences in your Flutter apps. Get creative, and let your imagination guide you!
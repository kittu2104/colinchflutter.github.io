---
layout: post
title: "Creating color splash effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Adding visual effects to images can greatly enhance the user experience in your Flutter app. One popular effect is the color splash effect, where a specific color is highlighted while the rest of the image appears in grayscale. In this blog post, we will explore how to create color splash effects using SkiaShadersMask in Flutter.

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Implementing the Color Splash Effect](#implementing-the-color-splash-effect)
- [Conclusion](#conclusion)

## Introduction
The **SkiaShadersMask** class in Flutter provides a way to apply graphical effects to images through shaders. Shaders define the visual properties of the image, such as colors, gradients, and textures. By utilizing shaders, we can easily create the color splash effect.

## Prerequisites
Before we begin, make sure you have the following installed:
- Flutter SDK
- Android Studio or any other Flutter-compatible IDE

## Getting Started
1. Create a new Flutter project by running the following command in your terminal:
```dart
flutter create color_splash
```

2. Navigate into the newly created project directory:
```dart
cd color_splash
```

3. Open the project in your preferred IDE.

4. Open the `pubspec.yaml` file and add the **flutter_svg** package as a dependency:
```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_svg: ^0.21.0
```

5. Run the following command to install the package:
```dart
flutter pub get
```

6. Replace the contents of the `lib/main.dart` file with the following code:
```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';
import 'dart:ui' as ui;

void main() {
  runApp(ColorSplashApp());
}

class ColorSplashApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Color Splash',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: ColorSplashPage(),
    );
  }
}

class ColorSplashPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Color Splash'),
      ),
      body: Center(
        child: ColorSplashImage(),
      ),
    );
  }
}

class ColorSplashImage extends StatefulWidget {
  @override
  _ColorSplashImageState createState() => _ColorSplashImageState();
}

class _ColorSplashImageState extends State<ColorSplashImage> {
  @override
  Widget build(BuildContext context) {
    return ShaderMask(
      shaderCallback: (Rect bounds) {
        return ui.GradientMask(
          shader: ui.Gradient.linear(
            Offset.zero,
            Offset(0, bounds.height / 2),
            [
              Colors.transparent,
              Colors.black,
            ],
          ),
          mask: SvgPicture.asset(
            'assets/image.svg',
            fit: BoxFit.cover,
          ).paintBounds,
        ).createShader(bounds);
      },
      child: SvgPicture.asset(
        'assets/image.svg',
        fit: BoxFit.cover,
      ),
    );
  }
}
```

7. Create a new folder called `assets` in the root directory of the project.

8. Place the SVG image you want to apply the color splash effect to inside the `assets` folder.

9. Open the `pubspec.yaml` file and add the following lines to include the assets in your project:
```yaml
flutter:
  assets:
    - assets/
```

10. Run the app on a compatible device or emulator with the following command:
```dart
flutter run
```

## Implementing the Color Splash Effect
To create a color splash effect, we use the **ShaderMask** widget provided by Flutter. In the **_ColorSplashImageState** widget's **build** method, we use the **shaderCallback** parameter to define the shader that will create the color splash effect.

Within the **shaderCallback** function, we use the **GradientMask** class from the **dart:ui** package to define a linear gradient to which we apply a mask. The mask is created using the SVG image provided as the input. Lastly, we create a shader using the **createShader** method of the **GradientMask** class.

The **ShaderMask** widget takes the **child** widget, which is the original SVG image, and applies the shader to it, resulting in the color splash effect.

## Conclusion
In this blog post, we learned how to create color splash effects using SkiaShadersMask in Flutter. By utilizing shaders and the ShaderMask widget, we can easily create visually appealing effects in our Flutter applications. Give it a try and enhance the visual experience of your app with color splash effects. Happy coding!

#### #Flutter #ColorSplash
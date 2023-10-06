---
layout: post
title: "Creating frosted glass effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to create a frosted glass effect using the `SkiaShaderMask` widget in Flutter. The frosted glass effect is commonly used in modern user interfaces to add a sense of depth and elegance.

To achieve this effect, we will rely on the `SkiaShaderMask` widget, which allows us to apply a custom shader to a specific region of the screen.

## Prerequisites
Before we begin, make sure you have the following prerequisites:

- Flutter SDK installed on your machine
- A basic understanding of Flutter widgets and shaders

## Steps to create a frosted glass effect

### Step 1: Set up a new Flutter project
Start by setting up a new Flutter project using the following command:

```bash
flutter create frosted_glass_app
```

### Step 2: Modify the main.dart file
Replace the code in the `lib/main.dart` file with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(FrostedGlassApp());
}

class FrostedGlassApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Frosted Glass App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: FrostedGlassPage(),
    );
  }
}

class FrostedGlassPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Frosted Glass Effect'),
      ),
      body: Center(
        child: Container(
          width: 200,
          height: 200,
          child: SkiaShaderMask(
            shaderCallback: (Rect bounds) {
              return LinearGradient(
                colors: [
                  Colors.transparent,
                  Colors.white.withOpacity(0.3),
                  Colors.white.withOpacity(0.3),
                  Colors.transparent,
                ],
                stops: [0.0, 0.1, 0.9, 1.0],
              ).createShader(bounds);
            },
            child: FlutterLogo(),
          ),
        ),
      ),
    );
  }
}
```

### Step 3: Run the app
Save the file and run the app using the following command:

```bash
flutter run
```

You should now see a frosted glass effect applied to the Flutter logo. The `SkiaShaderMask` widget uses a `LinearGradient` shader to create the frosted glass effect. By specifying transparent and semi-transparent colors in the gradient, we can control the transparency levels of the glass effect.

## Conclusion
In this tutorial, you learned how to create a frosted glass effect using the `SkiaShaderMask` widget in Flutter. This effect can be easily customized by changing the colors and stops of the gradient. Use this technique to add a touch of elegance to your Flutter user interfaces.

Happy coding!

#Flutter #FrostedGlassEffect
---
layout: post
title: "Creating retro effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

If you want to add a touch of retro to your Flutter application, you can use the SkiaShadersMask class to create a variety of cool effects. SkiaShadersMask is a powerful tool that allows you to apply image masks with customizable shaders to create unique and eye-catching visuals.

In this tutorial, we will walk through the process of using SkiaShadersMask to create a retro effect on an image in Flutter.

## Table of Contents
1. [Setting up the project](#setting-up-the-project)
2. [Creating the retro effect](#creating-the-retro-effect)
3. [Applying the effect to an image](#applying-the-effect-to-an-image)
4. [Conclusion](#conclusion)

## Setting up the project

Before we get started, make sure you have Flutter installed and set up on your machine. You will need a basic understanding of Flutter development to follow along with this tutorial.

To create a new Flutter project, run the following command in your terminal:

```
flutter create retro_effects
```

Navigate to the project directory:

```
cd retro_effects
```

Open the project in your favorite code editor.

## Creating the retro effect

Flutter provides a SkiaCanvas class that allows us to draw custom graphics. We'll use this to create a custom shader that simulates a retro effect.

Inside the `main.dart` file, add the following code to create a custom shader class:

```dart
import 'dart:ui';

class RetroShader extends Shader {
  RetroShader(Rect bounds) : super(bounds, _createShader());

  static ImageShader _createShader() {
    final imageBytes = File('assets/retro_mask.png').readAsBytesSync();
    final codec = await instantiateImageCodec(imageBytes);
    final frameInfo = await codec.getNextFrame();
    final image = frameInfo.image;
    return ImageShader(image, TileMode.repeated, TileMode.repeated, Float64List(6), Matrix4.identity().storage);
  }
}
```

Ensure that you have an image file named `retro_mask.png` in your assets folder. This image will act as a mask for the retro effect.

## Applying the effect to an image

Now that we have our custom shader class, let's apply the retro effect to an image.

Inside the `main.dart` file, replace the default `MyHomePage` class with the following code:

```dart
class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Retro Effects"),
      ),
      body: Center(
        child: ShaderMask(
          blendMode: BlendMode.modulate,
          shaderCallback: (rect) {
            return RetroShader(rect);
          },
          child: Image.asset(
            'assets/image.jpg',
            width: 300,
            height: 300,
            fit: BoxFit.cover,
          ),
        ),
      ),
    );
  }
}
```

In this code, we wrap our image widget with a `ShaderMask` widget. We set the `blendMode` to `BlendMode.modulate` to apply the retro effect. We also pass the `RetroShader` class to the `shaderCallback` property.

Finally, we display the image using the `Image.asset` widget, providing the path to our image file.

## Conclusion

By using the SkiaShadersMask class, we can easily add retro effects to our Flutter applications. We demonstrated how to create a custom shader and apply it as a mask to an image.

With a little creativity and experimentation, you can create unique retro effects that will make your Flutter app stand out. Have fun exploring the possibilities!

Happy coding! 🚀

##### #flutter #retroeffects
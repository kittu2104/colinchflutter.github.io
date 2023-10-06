---
layout: post
title: "Applying ASCII video effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this blog post, we will explore how to apply ASCII video effects to a video using SkiaShadersMask in Flutter. SkiaShadersMask is a powerful library that allows you to create various visual effects in your Flutter applications.

## Table of Contents
- [What is SkiaShadersMask?](#what-is-skiashadersmask)
- [Setting up the Project](#setting-up-the-project)
- [Applying ASCII Video Effects](#applying-ascii-video-effects)
- [Conclusion](#conclusion)

## What is SkiaShadersMask?

SkiaShadersMask is a library that provides an abstraction layer for creating and applying shaders in the Skia graphics library. Shaders are used to provide different effects, such as color transformations, blurs, distortions, and more.

## Setting up the Project

Before we begin, make sure you have Flutter installed on your machine. You can check the Flutter installation by running the following command in your terminal:

```
flutter doctor
```

To create a new Flutter project, run the following command:

```
flutter create ascii_video_effects
```

Once the project is created, open it in your preferred IDE. We will be using Visual Studio Code for this tutorial.

## Applying ASCII Video Effects

To apply ASCII video effects, we will be using the SkiaShadersMask library. Start by adding the following dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  skia_shaders_mask: ^0.1.0
```

Save the file and run the following command to fetch the dependencies:

```
flutter pub get
```

Now, let's create a new file called `ascii_video_effects.dart` and replace the default code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:skia_shaders_mask/skia_shaders_mask.dart';

class ASCIIVideoEffects extends StatefulWidget {
  @override
  _ASCIIVideoEffectsState createState() => _ASCIIVideoEffectsState();
}

class _ASCIIVideoEffectsState extends State<ASCIIVideoEffects> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('ASCII Video Effects'),
      ),
      body: Center(
        child: ShaderMask(
          shaderCallback: (Rect bounds) {
            return SkiaShaders.asciiShader();
          },
          blendMode: BlendMode.srcATop,
          child: Image.network(
            'https://example.com/video.mp4',
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

In the code above, we have created a `ASCIIVideoEffects` widget that extends `StatefulWidget`. The `_ASCIIVideoEffectsState` class defines the state for the widget and contains the build method where the visual elements are rendered.

Inside the build method, we have a `ShaderMask` widget. The `shaderCallback` parameter is set to the `SkiaShaders.asciiShader()` method, which returns the ASCII shader. The `blendMode` property is set to `BlendMode.srcATop`, which specifies how the shader should be blended with the image.

The `child` property of the `ShaderMask` widget is an `Image` widget that displays the video. Make sure to replace the placeholder URL ('https://example.com/video.mp4') with the URL of your video.

## Conclusion

In this blog post, we explored how to apply ASCII video effects to a video using SkiaShadersMask in Flutter. SkiaShadersMask provides a convenient way to create visually appealing effects in your Flutter applications.

By leveraging the power of SkiaShadersMask, you can enhance the visual experience of your videos and make them stand out. Experiment with different shaders and blend modes to create unique effects that captivate your users.

#flutter #videoeffects
---
layout: post
title: "Creating kaleidoscope video effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Video effects can add a captivating and unique touch to your Flutter applications. One such effect is the kaleidoscope effect, which creates fascinating and visually appealing patterns. In this tutorial, we will explore how to create kaleidoscope video effects using SkiaShadersMask in Flutter.

## What is SkiaShadersMask?

SkiaShadersMask is a powerful feature provided by the Skia graphics library, which Flutter relies on for rendering UI elements. It allows us to apply various effects and transformations to images and videos, including the kaleidoscope effect.

## Prerequisites

To follow along with this tutorial, ensure that you have the following prerequisites:

- Flutter SDK installed on your local machine
- A basic understanding of Flutter and Dart programming
- A code editor of your choice

## Setting up the project

1. Create a new Flutter project using the following command:

```dart
$ flutter create kaleidoscope_video_effects
```

2. Open the project in your preferred code editor.

3. Replace the contents of `lib/main.dart` with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:skia/shaders.dart';
import 'package:video_player/video_player.dart';

void main() {
  runApp(KaleidoscopeVideoApp());
}

class KaleidoscopeVideoApp extends StatefulWidget {
  @override
  _KaleidoscopeVideoAppState createState() => _KaleidoscopeVideoAppState();
}

class _KaleidoscopeVideoAppState extends State<KaleidoscopeVideoApp> {
  VideoPlayerController _videoPlayerController;
  bool _isPlaying = false;

  @override
  void initState() {
    super.initState();
    _videoPlayerController = VideoPlayerController.network(
      'https://example.com/video.mp4', // Replace with your video URL
    )..initialize().then((_) {
        setState(() {});
      });
  }

  @override
  void dispose() {
    _videoPlayerController.dispose();
    super.dispose();
  }

  Widget _buildKaleidoscopeVideo() {
    return SizedBox(
      width: double.infinity,
      child: ShaderMask(
        shaderCallback: (rect) {
          final videoTexture = _videoPlayerController.textureId;
          final mask = const KaleidoscopeShaderMask().createShader(rect);

          return ComposeShader(videoTexture, mask);
        },
        blendMode: BlendMode.srcOver,
        child: _videoPlayerController.value.isInitialized
            ? VideoPlayer(_videoPlayerController)
            : Container(),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Kaleidoscope Video Effects',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Kaleidoscope Video Effects'),
        ),
        body: Center(
          child: _buildKaleidoscopeVideo(),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            setState(() {
              _isPlaying ? _videoPlayerController.pause() : _videoPlayerController.play();
              _isPlaying = !_isPlaying;
            });
          },
          child: Icon(_isPlaying ? Icons.pause : Icons.play_arrow),
        ),
      ),
    );
  }
}
```

## Understanding the code

Let's walk through the code and understand how the kaleidoscope video effect is implemented:

1. Import the required packages: `material.dart`, `skia/shaders.dart`, and `video_player.dart`.

2. Define the `KaleidoscopeVideoApp` class, which extends `StatefulWidget`. We will implement the video effect inside this widget.

3. Initialize the `_videoPlayerController` in the `initState` method. Replace the video URL with the URL of the video you want to apply the kaleidoscope effect to.

4. Dispose the `_videoPlayerController` in the `dispose` method to release any resources used by the video player.

5. Implement the `_buildKaleidoscopeVideo` method, which returns the widget tree for the kaleidoscope video effect. Inside this method, we create a `ShaderMask`, which takes a `shaderCallback` and a `blendMode`. The `shaderCallback` method is responsible for creating the kaleidoscope effect shader using the `KaleidoscopeShaderMask`, which we will define shortly. The `blendMode` determines how the shaders blend with the video.

6. Finally, in the `build` method, we return a `MaterialApp` with the `Scaffold` widget. The `_buildKaleidoscopeVideo` method is used to display the video on the screen. A floating action button is added to control the video playback.

7. The `KaleidoscopeShaderMask` is a custom class that we will define next.

## Implementing the KaleidoscopeShaderMask

1. Create a new file named `kaleidoscope_shader_mask.dart` inside the `lib` directory.

2. Add the following code to the newly created file:

```dart
import 'package:flutter/foundation.dart';
import 'package:skia/pdf.dart';

class KaleidoscopeShaderMask {
  Shader createShader(Rect bounds) {
    final skiaShader = pdf.initKaleidoscopeShader(
      bounds.left,
      bounds.top,
      bounds.width,
      bounds.height,
      8, // Number of segments in the kaleidoscope effect
    );

    return skiaShader;
  }
}
```

3. Save the file.

## Running the application

To run the application, execute the following command in the terminal:

```dart
$ flutter run
```

If everything is set up correctly, you should see your Flutter application running with the kaleidoscope video effect applied.

## Conclusion

In this tutorial, we explored how to create kaleidoscope video effects using SkiaShadersMask in Flutter. By leveraging the Skia library, we were able to create captivating visuals and enhance the user experience in our applications. Feel free to experiment with different parameters and settings to create your own unique video effects.

#flutter #videoeffects
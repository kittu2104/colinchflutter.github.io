---
layout: post
title: "Adding video rotation and flipping during trimming in Flutter"
description: " "
date: 2023-10-03
tags: [flutterdevelopment]
comments: true
share: true
---

In mobile app development, it's common to have a feature where users can trim and edit videos. If you're using Flutter, you might want to provide additional options like rotating and flipping the video during the trimming process. In this article, we'll discuss how you can achieve this in Flutter using the `video_player` and `flutter_ffmpeg` packages.

## Step 1: Install Dependencies

First, let's start by adding the required dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_player: ^2.2.5
  flutter_ffmpeg: ^1.2.0
```

After updating the dependencies, run `flutter packages get` to download and install them.

## Step 2: Add Video Player Widget

Next, let's add the video player widget to your Flutter app. You can use the `video_player` package to achieve this. Here's an example of how to display a video in your app:

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';

class VideoPlayerScreen extends StatefulWidget {
  final String videoPath;

  VideoPlayerScreen({required this.videoPath});

  @override
  _VideoPlayerScreenState createState() => _VideoPlayerScreenState();
}

class _VideoPlayerScreenState extends State<VideoPlayerScreen> {
  late VideoPlayerController _controller;

  @override
  void initState() {
    super.initState();
    _controller = VideoPlayerController.file(File(widget.videoPath))
      ..initialize().then((_) {
        setState(() {});
      });
  }

  @override
  void dispose() {
    super.dispose();
    _controller.dispose();
  }

  @override
  Widget build(BuildContext context) {
    if (!_controller.value.isInitialized) {
      return Container();
    }

    return AspectRatio(
      aspectRatio: _controller.value.aspectRatio,
      child: VideoPlayer(_controller),
    );
  }
}
```

## Step 3: Implement Video Transformation

To enable video rotation and flipping, we'll use the `flutter_ffmpeg` package. This package provides an interface to FFmpeg, a powerful multimedia framework. Here's an example of how you can rotate and flip a video:

```dart
import 'package:flutter_ffmpeg/flutter_ffmpeg.dart';

class VideoUtils {
  static Future<void> rotateVideo(String inputPath, String outputPath, int degrees) async {
    final FlutterFFmpeg _flutterFFmpeg = FlutterFFmpeg();

    final String command = "-i $inputPath -vf \"transpose=$degrees\" -c:a copy $outputPath";
    return _flutterFFmpeg.execute(command);
  }

  static Future<void> flipVideo(String inputPath, String outputPath, bool horizontally, bool vertically) async {
    final FlutterFFmpeg _flutterFFmpeg = FlutterFFmpeg();

    String flip = '';
    if (horizontally) flip += 'hflip';
    if (vertically) {
      if (flip.isNotEmpty) flip += ',';
      flip += 'vflip';
    }

    final String command = "-i $inputPath -vf \"$flip\" -c:a copy $outputPath";
    return _flutterFFmpeg.execute(command);
  }
}
```

In the `rotateVideo` method, we specify the input and output paths, along with the number of degrees to rotate (-90, 90, 180, etc.). Similarly, in the `flipVideo` method, we specify the input and output paths, along with the horizontal and vertical flipping options.

## Step 4: Integrate Video Transformation with Trimming

Finally, you can integrate video transformation with the trimming feature in your app. When the user rotates or flips the video, apply the desired transformation using the `VideoUtils` methods. After that, you can use the transformed video for trimming and further editing.

```dart
void trimAndEditVideo() async {
  // Apply video transformation using VideoUtils.rotateVideo or VideoUtils.flipVideo

  // Perform video trimming and other editing operations
}
```

By integrating these steps, you can add video rotation and flipping options during the trimming process in your Flutter app. This way, users will have more control over editing their videos according to their preferences.

#flutter #flutterdevelopment
---
layout: post
title: "Creating a video player with custom aspect ratios in Flutter"
description: " "
date: 2023-09-19
tags: [videoplayer]
comments: true
share: true
---

In this tutorial, we will learn how to create a video player with custom aspect ratios in Flutter. By default, the Flutter video player package does not provide a way to set custom aspect ratios for videos. However, we can achieve this by using a combination of the video_player package and the aspect_ratio package.

## Prerequisites

Before we begin, make sure you have Flutter and Dart installed on your machine. You can check the Flutter installation by running the following command in your terminal:

```bash
flutter doctor
```

## Steps

### Step 1: Add dependencies

To get started, open your Flutter project and go to the `pubspec.yaml` file. Add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_player: ^2.2.0
  aspect_ratio: ^0.8.0
```

Save the file and run `flutter pub get` on the terminal to download the dependencies.

### Step 2: Import packages

Open your Dart file and import the required packages:

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';
import 'package:aspect_ratio/aspect_ratio.dart';
```

### Step 3: Create a video player widget

Create a stateful widget called `CustomVideoPlayer` that extends `StatefulWidget`:

```dart
class CustomVideoPlayer extends StatefulWidget {
  final String videoUrl;

  const CustomVideoPlayer({Key? key, required this.videoUrl}) : super(key: key);

  @override
  _CustomVideoPlayerState createState() => _CustomVideoPlayerState();
}
```

Inside the `_CustomVideoPlayerState` class, define a `VideoPlayerController` instance and override the `initState` method to initialize the controller with the given video URL:

```dart
class _CustomVideoPlayerState extends State<CustomVideoPlayer> {
  late final VideoPlayerController _videoController;

  @override
  void initState() {
    super.initState();
    _videoController = VideoPlayerController.network(widget.videoUrl)
      ..initialize().then((_) {
        setState(() {});
      });
  }

  @override
  Widget build(BuildContext context) {
    if (!_videoController.value.isInitialized) {
      return CircularProgressIndicator();
    }

    return AspectRatio(
      aspectRatio: _videoController.value.aspectRatio,
      child: VideoPlayer(_videoController),
    );
  }

  @override
  void dispose() {
    _videoController.dispose();
    super.dispose();
  }
}
```

### Step 4: Use the custom video player

Now, you can use the `CustomVideoPlayer` widget in your application. Pass the video URL to the widget as a parameter:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Video Player Demo',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Custom Video Player'),
        ),
        body: Center(
          child: CustomVideoPlayer(
            videoUrl: 'https://example.com/video.mp4',
          ),
        ),
      ),
    );
  }
}
```

That's it! You have successfully created a video player with custom aspect ratios in Flutter. Now you can customize the `AspectRatio` widget to achieve the desired video dimensions.

Remember to `dispose()` the `VideoPlayerController` when it is no longer needed to avoid memory leaks.

## Conclusion

In this tutorial, we learned how to create a video player with custom aspect ratios in Flutter. By combining the `video_player` and `aspect_ratio` packages, we successfully implemented a custom video player that can display videos with different aspect ratios. Feel free to explore further and enhance the player with additional features.

#flutter #videoplayer
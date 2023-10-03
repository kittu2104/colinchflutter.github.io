---
layout: post
title: "Creating a video trimming progress bar in Flutter"
description: " "
date: 2023-10-03
tags: [Flutter, VideoTrimming, ProgressBar]
comments: true
share: true
---

Trimming videos is a common feature in video editing applications. In this tutorial, we will learn how to create a video trimming progress bar in Flutter, allowing users to visually select the portion of the video they want to keep.

## Prerequisites

Before we begin, make sure you have Flutter installed on your machine. You can follow the official Flutter installation guide for your platform.

## Dependencies

We will be using the `video_player` and `flutter_slider` packages to implement the video trimming progress bar. Add these dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_player: ^2.2.1
  flutter_slider: ^2.0.0
```

## Implementing the Video Trimming Progress Bar

1. Import the necessary packages in your Dart file:

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';
import 'package:flutter_slider/flutter_slider.dart';
```

2. Create a class that extends `StatefulWidget`:

```dart
class VideoTrimmingProgressBar extends StatefulWidget {
  final String videoPath;

  const VideoTrimmingProgressBar({required this.videoPath});

  @override
  _VideoTrimmingProgressBarState createState() =>
      _VideoTrimmingProgressBarState();
}
```

3. Define the state class:

```dart
class _VideoTrimmingProgressBarState
    extends State<VideoTrimmingProgressBar> {
  late VideoPlayerController _videoPlayerController;
  double _trimStart = 0;
  double _trimEnd = 0;

  @override
  void initState() {
    super.initState();
    _videoPlayerController =
        VideoPlayerController.network(widget.videoPath)
          ..addListener(() => setState(() {}));
    _videoPlayerController.initialize().then((_) {
      setState(() {});
      _videoPlayerController.setLooping(true);
      _videoPlayerController.play();
    });
  }

  @override
  void dispose() {
    _videoPlayerController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Video Trimming Progress Bar'),
      ),
      body: _videoPlayerController.value.isInitialized
          ? Column(
              children: [
                AspectRatio(
                  aspectRatio: _videoPlayerController.value.aspectRatio,
                  child: VideoPlayer(_videoPlayerController),
                ),
                Container(
                  padding: EdgeInsets.symmetric(horizontal: 16.0),
                  child: Slider(
                    min: 0,
                    max: _videoPlayerController.value.duration.inMilliseconds.toDouble(),
                    onChanged: (value) {
                      setState(() {
                        _trimStart = value;
                      });
                    },
                    onChangeEnd: (value) {
                      setState(() {
                        _trimStart = value;
                        _videoPlayerController.seekTo(Duration(milliseconds: _trimStart.toInt()));
                      });
                    },
                    value: _trimStart,
                  ),
                ),
              ],
            )
          : Center(child: CircularProgressIndicator()),
    );
  }
}
```

## Using the Video Trimming Progress Bar

To use the `VideoTrimmingProgressBar` widget, you need to pass the video path as a parameter. Here's an example of how you can use it:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Video Trimming Progress Bar Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: VideoTrimmingProgressBar(
        videoPath: 'https://example.com/video.mp4',
      ),
    );
  }
}
```

## Conclusion

In this tutorial, we learned how to create a video trimming progress bar in Flutter using the `video_player` and `flutter_slider` packages. With this component, users can easily select the desired portion of a video to keep. By customizing the UI or adding additional functionalities, you can enhance the trimming experience in your app.

**#Flutter #VideoTrimming #ProgressBar**
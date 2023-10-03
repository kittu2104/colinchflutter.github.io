---
layout: post
title: "Adding a video playback scrubber during trimming in Flutter"
description: " "
date: 2023-10-03
tags: []
comments: true
share: true
---

When building a video editing application in Flutter, it is often necessary to allow users to trim and preview the video before saving or sharing it. One essential feature for this is the video playback scrubber, which allows users to control the position of the video playback.

In this blog post, we will explore how to implement a video playback scrubber during trimming in Flutter using the **video_player** package and **Slider** widget.

## Prerequisites

Before getting started, ensure that you have the **video_player** package added to your Flutter project. You can do this by adding the following line to your **pubspec.yaml** file:

```yaml
dependencies:
  video_player: ^2.2.5
```

## Implementation

1. Import the required packages:

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';
```

2. Create a **VideoPlayerController** instance and initialize it with the video file:

```dart
VideoPlayerController _controller;

@override
void initState() {
  super.initState();
  _controller = VideoPlayerController.asset('path_to_video_file.mp4')
    ..initialize().then((_) {
      setState(() {});
    });
}
```

3. Build the UI with a **VideoPlayer** widget and a **Slider** widget:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text('Video Trimmer'),
    ),
    body: _controller.value.isInitialized
        ? Column(
            children: [
              AspectRatio(
                aspectRatio: _controller.value.aspectRatio,
                child: VideoPlayer(_controller),
              ),
              Slider(
                min: 0.0,
                max: _controller.value.duration.inSeconds.toDouble(),
                value: _controller.value.position.inSeconds.toDouble(),
                onChanged: (value) {
                  setState(() {
                    _controller.seekTo(Duration(seconds: value.toInt()));
                  });
                },
              ),
            ],
          )
        : Container(),
    floatingActionButton: FloatingActionButton(
      onPressed: () {
        // Add your logic to save or share the trimmed video
      },
      child: Icon(Icons.check),
    ),
  );
}
```

4. Dispose of the **VideoPlayerController** instance:

```dart
@override
void dispose() {
  _controller.dispose();
  super.dispose();
}
```

## Conclusion

In this tutorial, we have learned how to implement a video playback scrubber during trimming in Flutter. By using the **video_player** package and the **Slider** widget, we can provide users with a seamless video trimming experience.
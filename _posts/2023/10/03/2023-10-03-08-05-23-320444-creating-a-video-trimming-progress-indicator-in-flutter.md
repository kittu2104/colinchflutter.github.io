---
layout: post
title: "Creating a video trimming progress indicator in Flutter"
description: " "
date: 2023-10-03
tags: [videotrimming]
comments: true
share: true
---

When working with video editing functionality in a Flutter application, it is often useful to include a progress indicator to show the user the current progress of trimming the video. In this tutorial, we will walk through the steps of creating a video trimming progress indicator in Flutter.

## Step 1: Installing Dependencies

The first step is to install the required dependencies. In your `pubspec.yaml` file, add the following lines:

```yaml
dependencies:
  video_player: ^2.1.6
```

Then, run `flutter pub get` to fetch the dependencies.

## Step 2: Creating a Video Trimming Progress Indicator Widget

Next, we will create a reusable Flutter widget that represents the video trimming progress indicator. Here's an example implementation:

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';

class VideoTrimmingProgressIndicator extends StatefulWidget {
  final VideoPlayerController controller;

  VideoTrimmingProgressIndicator({required this.controller});

  @override
  _VideoTrimmingProgressIndicatorState createState() => _VideoTrimmingProgressIndicatorState();
}

class _VideoTrimmingProgressIndicatorState extends State<VideoTrimmingProgressIndicator> {
  late double _progress;

  @override
  void initState() {
    super.initState();
    _progress = 0;
    widget.controller.addListener(() {
      setState(() {
        final currentPosition = widget.controller.value.position.inMilliseconds;
        final videoDuration = widget.controller.value.duration.inMilliseconds;
        _progress = currentPosition / videoDuration;
      });
    });
  }

  @override
  Widget build(BuildContext context) {
    return LinearProgressIndicator(value: _progress);
  }
}
```

In the above code, we create a `VideoTrimmingProgressIndicator` widget that takes a `VideoPlayerController` as a parameter. The widget keeps track of the progress by updating the `_progress` variable whenever the video position changes. We then use a `LinearProgressIndicator` to display the progress visually.

## Step 3: Using the Video Trimming Progress Indicator

To use the `VideoTrimmingProgressIndicator` widget in your application, simply create an instance of `VideoPlayerController` and pass it to the widget as shown below:

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final VideoPlayerController controller = VideoPlayerController.network('https://example.com/video.mp4');

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Video Trimming Progress Indicator',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Video Trimming Progress Indicator'),
        ),
        body: Center(
          child: VideoTrimmingProgressIndicator(controller: controller),
        ),
      ),
    );
  }

  @override
  void dispose() {
    controller.dispose();
    super.dispose();
  }
}
```

In the above code, we create a `MyApp` widget that initializes a `VideoPlayerController` and sets it as the `controller` property of the `VideoTrimmingProgressIndicator` widget. The progress indicator is then displayed in the center of the app's body.

## Conclusion

In this tutorial, we have created a video trimming progress indicator in Flutter using the `video_player` package. You can now integrate this progress indicator into your video editing applications to provide a visual representation of the video trimming progress.

#flutter #videotrimming
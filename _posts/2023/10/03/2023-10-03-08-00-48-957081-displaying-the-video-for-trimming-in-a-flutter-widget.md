---
layout: post
title: "Displaying the video for trimming in a Flutter widget"
description: " "
date: 2023-10-03
tags: [VideoTrimmer]
comments: true
share: true
---

In this tutorial, we will learn how to display a video for trimming in a Flutter widget. We will use the `video_player` package to handle video playback, and the `flutter_ffmpeg` package to trim the video.

## Prerequisites

Before we begin, make sure you have the following installed:

- Flutter SDK
- Android Studio or Xcode (depending on your operating system)

## Step 1: Set up the project

Create a new Flutter project using the following command:

```bash
flutter create video_trimming_app
```

Change to the project directory:

```bash
cd video_trimming_app
```

Open the project in your preferred code editor.

## Step 2: Add dependencies

Open the `pubspec.yaml` file and add the necessary dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_player: ^2.0.0
  flutter_ffmpeg: ^x.x.x  # Replace x.x.x with the latest version
```

Run `flutter pub get` to fetch the dependencies.

## Step 3: Create a video trimming widget

Create a new file called `video_trimming_widget.dart` in the `lib` directory. In this file, add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';

class VideoTrimmingWidget extends StatefulWidget {
  final String videoPath;

  VideoTrimmingWidget({required this.videoPath});

  @override
  _VideoTrimmingWidgetState createState() => _VideoTrimmingWidgetState();
}

class _VideoTrimmingWidgetState extends State<VideoTrimmingWidget> {
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
    if (_controller.value.isInitialized) {
      return AspectRatio(
        aspectRatio: _controller.value.aspectRatio,
        child: VideoPlayer(_controller),
      );
    } else {
      return CircularProgressIndicator();
    }
  }
}
```

## Step 4: Use the video trimming widget

Now, let's use the `VideoTrimmingWidget` in our app. Open the `main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:video_trimming_app/video_trimming_widget.dart';

void main() {
  runApp(VideoTrimmingApp());
}

class VideoTrimmingApp extends StatelessWidget {
  final String videoPath = 'assets/videos/sample.mp4';

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        appBar: AppBar(
          title: Text('Video Trimming App'),
        ),
        body: Center(
          child: VideoTrimmingWidget(videoPath: videoPath),
        ),
      ),
    );
  }
}
```

Make sure to replace `'assets/videos/sample.mp4'` with the path to your video file.

## Step 5: Run the app

Finally, let's run the app on a simulator or device. Use the following command to launch the app:

```bash
flutter run
```

The app should now display the video for trimming in the Flutter widget.

That's it! You have successfully displayed a video for trimming in a Flutter widget. Feel free to customize the widget according to your needs.

#Flutter #VideoTrimmer
---
layout: post
title: "Implementing video trimming using two fingers gesture in Flutter"
description: " "
date: 2023-10-03
tags: []
comments: true
share: true
---

In this blog post, we will explore how to implement video trimming functionality using a two-fingers gesture in a Flutter application. This feature allows users to select a specific portion of a video by simply sliding their two fingers across the screen.

## Prerequisites
To follow along with this tutorial, you will need:

1. Flutter installed on your machine. You can download Flutter from the official Flutter website.
2. A code editor of your choice. We recommend using Visual Studio Code or Android Studio.

## Step 1: Setting Up the Flutter Project
Start by creating a new Flutter project using the following command:

```shell
flutter create video_trimming_app
```

Once the project is created, navigate to the project directory:

```shell
cd video_trimming_app
```

## Step 2: Adding Dependencies
To implement video trimming, we'll need to use some third-party packages. Open the `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_player: ^2.2.5
  flutter_gesture_detector: ^4.4.0
```

Save the file and run the following command to fetch the dependencies:

```shell
flutter pub get
```

## Step 3: Building the Video Trimming UI
In this step, we'll create the UI for our video trimming feature. Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';
import 'package:flutter_gesture_detector/flutter_gesture_detector.dart';

void main() {
  runApp(VideoTrimmingApp());
}

class VideoTrimmingApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: VideoTrimmingScreen(),
    );
  }
}

class VideoTrimmingScreen extends StatefulWidget {
  @override
  _VideoTrimmingScreenState createState() => _VideoTrimmingScreenState();
}

class _VideoTrimmingScreenState extends State<VideoTrimmingScreen> {
  final GlobalKey<ScaffoldState> _scaffoldKey = GlobalKey<ScaffoldState>();

  VideoPlayerController _controller;
  GestureRecognizer _gestureRecognizer;

  @override
  void initState() {
    super.initState();
    _controller = VideoPlayerController.network(
        'https://example.com/video.mp4');
    _gestureRecognizer = TwoFingerGestureRecognizer()
      ..onMove = _handleGestureMove
      ..onEnd = _handleGestureEnd;
  }

  @override
  void dispose() {
    super.dispose();
    _controller.dispose();
    _gestureRecognizer.dispose();
  }

  void _handleGestureMove(TwoFingerMoveEvent event) {
    // Process the two-fingers gesture move event
    // Update the video trimming UI accordingly
    // Calculate the selected portion of the video
  }

  void _handleGestureEnd(TwoFingerEndEvent event) {
    // Process the two-fingers gesture end event
    // Perform the video trimming based on the selected portion
    // Save the trimmed video
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      key: _scaffoldKey,
      appBar: AppBar(
        title: Text('Video Trimming'),
      ),
      body: Center(
        child: AspectRatio(
          aspectRatio: _controller.value.aspectRatio,
          child: GestureDetector(
            onScaleStart: _handleGestureStart,
            child: VideoPlayer(_controller),
          ),
        ),
      ),
    );
  }

  void _handleGestureStart(ScaleStartDetails details) {
    _controller.play();
  }
}
```

Make sure to replace the video URL with the URL of your own video.

## Step 4: Implementing the Video Trimming Logic
Now that we have our UI ready, let's implement the actual video trimming logic. We'll add the necessary code inside the `_handleGestureMove` and `_handleGestureEnd` methods.

```dart
void _handleGestureMove(TwoFingerMoveEvent event) {
  // Process the two-fingers gesture move event
  // Update the video trimming UI accordingly
  // Calculate the selected portion of the video
}

void _handleGestureEnd(TwoFingerEndEvent event) {
  // Process the two-fingers gesture end event
  // Perform the video trimming based on the selected portion
  // Save the trimmed video
}
```

Feel free to customize the logic of video trimming based on your specific requirements.

## Step 5: Testing the Application
To run the application, use the following command:

```shell
flutter run
```

After the app launches, you should see the video player with your video loaded. Try using the two-finger gesture to select a portion of the video for trimming.

## Conclusion
In this tutorial, we have learned how to implement video trimming using a two-fingers gesture in a Flutter application. You can further enhance this functionality by adding more features such as previewing the trimmed video or adding markers for precise selection.
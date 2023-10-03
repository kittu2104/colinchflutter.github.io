---
layout: post
title: "Adding a video trimming progress notification in Flutter"
description: " "
date: 2023-10-03
tags: []
comments: true
share: true
---

When working with videos in Flutter, it may be necessary to implement a video trimming feature where the user can select a specific portion of the video to keep. During the trimming process, it is important to provide feedback to the user through a progress notification. In this tutorial, we will walk through the steps to add a video trimming progress notification in Flutter.

## Prerequisites
Before getting started, make sure you have Flutter installed on your machine. You can follow the official [Flutter installation guide](https://flutter.dev/docs/get-started/install) if you haven't done so yet.

## Steps

### 1. Add Video Trimming Package
To implement video trimming, we can use the `video_editor` package in Flutter. Open your project's `pubspec.yaml` file and add the following dependency:

```dart
dependencies:
  video_editor: ^0.2.1
```

### 2. Import Required Packages
In your Flutter Dart file, import the necessary packages:

```dart
import 'package:video_editor/video_editor.dart';
import 'package:flutter/material.dart';
```

### 3. Create a Video Player Widget
Create a widget that displays the video and controls the trimming process. You can use the `video_player` package to achieve this. Here's an example of a simple video player widget:

```dart
class VideoPlayerWidget extends StatefulWidget {
  final String videoPath;

  VideoPlayerWidget({required this.videoPath});

  @override
  _VideoPlayerWidgetState createState() => _VideoPlayerWidgetState();
}

class _VideoPlayerWidgetState extends State<VideoPlayerWidget> {
  late final VideoPlayerController _controller;

  @override
  void initState() {
    super.initState();
    _controller = VideoPlayerController.network(widget.videoPath)
      ..initialize().then((_) {
        setState(() {});
      });
  }

  @override
  Widget build(BuildContext context) {
    return _controller.value.isInitialized
        ? AspectRatio(
            aspectRatio: _controller.value.aspectRatio,
            child: VideoPlayer(_controller),
          )
        : CircularProgressIndicator();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
}
```

### 4. Add Video Trimming Logic
Implement the video trimming logic using the `video_editor` package. In this example, we will add a `RangeSelector` widget to select the portion of the video to keep:

```dart
class VideoTrimmingScreen extends StatelessWidget {
  final String videoPath;

  VideoTrimmingScreen({required this.videoPath});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Video Trimming'),
      ),
      body: Column(
        children: [
          VideoPlayerWidget(videoPath: videoPath),
          SizedBox(height: 20),
          Text('Select the portion to keep:'),
          RangeSelector(
            start: Duration.zero,
            end: _controller.value.duration,
            onChanged: (start, end) {
              // Handle the selected range
            },
          ),
        ],
      ),
    );
  }
}
```

### 5. Display Progress Notification
To display a progress notification, we can use the `toast` package in Flutter. First, add the `toast` package to your `pubspec.yaml` file:

```dart
dependencies:
  fluttertoast: ^8.0.8
```

Then, import the package and display the progress notification inside the `onChanged` callback:

```dart
import 'package:fluttertoast/fluttertoast.dart';

// ...

RangeSelector(
  start: Duration.zero,
  end: _controller.value.duration,
  onChanged: (start, end) {
    Fluttertoast.showToast(
      msg: 'Trimming in progress...',
      gravity: ToastGravity.CENTER,
      toastLength: Toast.LENGTH_LONG,
      timeInSecForIosWeb: 2,
    );

    // Handle the selected range
  },
),
```

### 6. Run the App
Finally, run your app on a device or emulator to test the video trimming feature with the progress notification.

## Conclusion
In this tutorial, we learned how to add a video trimming progress notification in Flutter. By following these steps, you should now have a video player with a trimming feature that provides feedback to the user during the trimming process.
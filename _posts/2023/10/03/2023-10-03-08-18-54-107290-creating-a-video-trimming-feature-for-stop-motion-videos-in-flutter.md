---
layout: post
title: "Creating a video trimming feature for stop motion videos in Flutter"
description: " "
date: 2023-10-03
tags: [flutter, stopmotion]
comments: true
share: true
---

Stop motion videos are a unique and creative way to tell stories or showcase products. One common requirement in stop motion video editing is the ability to trim the video and remove unwanted frames. In this blog post, we will learn how to create a video trimming feature for stop motion videos using Flutter.

## Prerequisites

Before we get started, make sure you have Flutter installed on your machine. You can download and install Flutter from the official Flutter website. Also, ensure that you have a basic knowledge of Flutter and Dart programming.

## Getting Started

First, let's create a new Flutter project by running the following command in your terminal:

```bash
flutter create stop_motion_trimming
cd stop_motion_trimming
```

## Adding Dependencies

To work with video manipulation, we need to add the following packages to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_player: ^2.0.0
  ffmpeg_flutter: ^2.0.0
  file_picker: ^4.0.0
```

After adding the dependencies, run `flutter pub get` to fetch and download them.

## Designing the User Interface

Next, let's design the user interface for our video trimming feature. For simplicity, we will have a single screen with a video player widget, a slider for selecting the start and end points, and buttons for trimming and saving the video.

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';

class VideoTrimmerScreen extends StatefulWidget {
  @override
  _VideoTrimmerScreenState createState() => _VideoTrimmerScreenState();
}

class _VideoTrimmerScreenState extends State<VideoTrimmerScreen> {
  VideoPlayerController _videoController;
  double _startPoint = 0.0;
  double _endPoint = 1.0;

  @override
  void initState() {
    super.initState();
    _videoController = VideoPlayerController.network(
        'https://example.com/stop_motion_video.mp4')
      ..initialize().then((_) {
        setState(() {});
      });
  }

  @override
  void dispose() {
    super.dispose();
    _videoController.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Stop Motion Video Trimmer'),
      ),
      body: _videoController.value.isInitialized
          ? Column(
              children: [
                AspectRatio(
                  aspectRatio: _videoController.value.aspectRatio,
                  child: VideoPlayer(_videoController),
                ),
                Slider(
                  value: _startPoint,
                  min: 0.0,
                  max: 1.0,
                  onChanged: (value) {
                    setState(() {
                      _startPoint = value;
                    });
                  },
                ),
                Slider(
                  value: _endPoint,
                  min: 0.0,
                  max: 1.0,
                  onChanged: (value) {
                    setState(() {
                      _endPoint = value;
                    });
                  },
                ),
                RaisedButton(
                  onPressed: () {
                    // Trim the video using ffmpeg_flutter package
                  },
                  child: Text('Trim Video'),
                ),
                RaisedButton(
                  onPressed: () {
                    // Save the trimmed video using file_picker package
                  },
                  child: Text('Save Video'),
                ),
              ],
            )
          : Center(
              child: CircularProgressIndicator(),
            ),
    );
  }
}
```

## Trimming the Video

To trim the video, we will use the `ffmpeg_flutter` package. This package provides a Flutter API for working with FFmpeg commands. Inside the 'Trim Video' button's `onPressed` callback, we can use the `executeWithArguments` method to trim the video based on the selected start and end points.

```dart
import 'package:ffmpeg_flutter/ffmpeg_flutter.dart';

...

RaisedButton(
  onPressed: () async {
    final ffmpeg = await getFFmpeg();
    final inputPath = _videoController.dataSource;
    final outputPath = 'path/to/trimmed_video.mp4';

    final startTimestamp = _startPoint * _videoController.value.duration.inSeconds;
    final endTimestamp = _endPoint * _videoController.value.duration.inSeconds;

    final arguments = ['-i', inputPath, '-ss', startTimestamp.toString(), '-to', endTimestamp.toString(), outputPath];
    final result = await ffmpeg.executeWithArguments(arguments);

    if (result == 0) {
      // Video successfully trimmed
      print('Video trimmed and saved to $outputPath');
    } else {
      // Error trimming the video
      print('Error trimming the video');
    }
  },
  child: Text('Trim Video'),
),
...
```

## Saving the Trimmed Video

To save the trimmed video, we will use the `file_picker` package. This package allows us to pick a file from the device's storage and save the trimmed video at the desired location. Inside the 'Save Video' button's `onPressed` callback, we can use the `FilePicker` class to pick a storage location and then copy the trimmed video file to that location.

```dart
import 'package:file_picker/file_picker.dart';

...

RaisedButton(
  onPressed: () async {
    final newPath = await FilePicker.getDirectoryPath();
    final outputPath = '$newPath/trimmed_video.mp4';

    await File(outputPath).writeAsBytes(await File('path/to/trimmed_video.mp4').readAsBytes());
      
    print('Video saved to $outputPath');
  },
  child: Text('Save Video'),
),
...
```

## Conclusion

In this blog post, we learned how to create a video trimming feature for stop motion videos using Flutter. We discussed how to play the video, select start and end points using sliders, and trim the video using FFmpeg. We also covered how to save the trimmed video using the file_picker package. Feel free to further enhance this feature by adding additional functionalities such as previewing the trimmed video or applying filters to the video frames.

\#flutter \#stopmotion
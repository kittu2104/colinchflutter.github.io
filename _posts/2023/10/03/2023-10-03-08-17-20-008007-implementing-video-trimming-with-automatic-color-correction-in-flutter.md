---
layout: post
title: "Implementing video trimming with automatic color correction in Flutter"
description: " "
date: 2023-10-03
tags: [video, trimming, colorcorrection]
comments: true
share: true
---

In this blog post, we will discuss how to implement video trimming with automatic color correction in a Flutter application. 

## Introduction

Videos have become an integral part of modern applications, and often, we need to provide users with the ability to trim videos before uploading or sharing them. Additionally, to enhance the video quality, automatic color correction can be applied to make the videos look more vibrant and appealing. 

## Prerequisites

Before we dive into the implementation, make sure you have the following prerequisites:

- Flutter SDK installed on your machine
- Basic knowledge of Dart and Flutter

## Getting Started

To get started, we need to include the required dependencies in our **pubspec.yaml** file:

```yaml
dependencies:
  flutter_video_trimmer: ^1.5.0
  flutter_video_processing: ^0.1.2
```

Once the dependencies are added, run `flutter pub get` to fetch them.

## Implementing Video Trimming

First, import the required packages and classes:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_video_trimmer/flutter_video_trimmer.dart';
```

Next, create a `VideoTrimmer` instance using the `flutter_video_trimmer` package:

```dart
final Trimmer _trimmer = Trimmer();
```

Now, let's create a UI for the video trimming screen. We can use the `VideoTrimmer` widget provided by the package:

```dart
Future<void> _openTrimmingScreen() async {
  final File videoFile = // Get the video file somehow
  
  if (videoFile != null) {
    await _trimmer.loadVideo(videoFile: videoFile);
    
    showDialog(
      context: context,
      builder: (_) => VideoViewerDialog(
        trimmer: _trimmer,
      ),
    );
  }
}
```

In the above code, `_openTrimmingScreen` method is responsible for showing a dialog with the video trimming UI. The `VideoViewerDialog` is a custom dialog that we need to implement.

```dart
class VideoViewerDialog extends StatefulWidget {
  final Trimmer trimmer;
  
  const VideoViewerDialog({Key? key, required this.trimmer}) : super(key: key);
  
  @override
  _VideoViewerDialogState createState() => _VideoViewerDialogState();
}

class _VideoViewerDialogState extends State<VideoViewerDialog> {
  final TextEditingController _startTextController = TextEditingController();
  final TextEditingController _endTextController = TextEditingController();
  
  String _startTime = '00:00:00';
  String _endTime = '00:00:00';
  
  @override
  void initState() {
    super.initState();
    
    _startTextController.text = _startTime;
    _endTextController.text = _endTime;
  }
  
  @override
  void dispose() {
    _startTextController.dispose();
    _endTextController.dispose();
    
    super.dispose();
  }
  
  @override
  Widget build(BuildContext context) {
    return AlertDialog(
      title: const Text('Video Trimmer'),
      content: Column(
        children: [
          TextField(
            controller: _startTextController,
            onChanged: (value) {
              setState(() {
                _startTime = value;
              });
            },
          ),
          TextField(
            controller: _endTextController,
            onChanged: (value) {
              setState(() {
                _endTime = value;
              });
            },
          ),
          VideoViewer(
            trimmer: true,
            viewerHeight: 200,
            viewerWidth: double.infinity,
            startTime: _startTime,
            endTime: _endTime,
            videoProvider: widget.trimmer.videoPlayerProvider,
          ),
        ],
      ),
      actions: [
        TextButton(
          onPressed: () async {
            await widget.trimmer.saveTrimmedVideo();
            Navigator.of(context).pop();
          },
          child: const Text('Save'),
        ),
        TextButton(
          onPressed: () {
            Navigator.of(context).pop();
          },
          child: const Text('Cancel'),
        ),
      ],
    );
  }
}
```

In the above code, we create a custom dialog widget called `VideoViewerDialog`. It allows users to set the start and end time of the video trimming using text fields. The video preview is displayed using the `VideoViewer` widget provided by the `flutter_video_trimmer` package.

## Implementing Automatic Color Correction

To implement automatic color correction, we will use the `flutter_video_processing` package. First, import the required packages and classes:

```dart
import 'package:flutter_video_processing/flutter_video_processing.dart';
```

Then, update the `saveTrimmedVideo` method in the `VideoViewerDialog` class:

```dart
await widget.trimmer.saveTrimmedVideo(concurrent: true);
final editedVideoPath = widget.trimmer.trimmedFilePath;
final video = FlutterVideoProcessing.postProduction(editedVideoPath);
final correctedVideoPath = await video.adjustWithFilter(FilterType.colorCorrection);

print('Corrected video save to: $correctedVideoPath');
```

In the above code, after saving the trimmed video, we retrieve the trimmed file path from the `VideoTrimmer` instance. We then create a `FlutterVideoProcessing` object with the trimmed file path and apply the `colorCorrection` filter using the `adjustWithFilter` method. The resulting corrected video path is then printed.

## Conclusion

In this blog post, we learned how to implement video trimming with automatic color correction in a Flutter application. We used the `flutter_video_trimmer` package to handle video trimming, and the `flutter_video_processing` package for automatic color correction. Feel free to explore these packages further and enhance the video editing capabilities in your Flutter apps!

#flutter #video #trimming #colorcorrection
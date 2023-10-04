---
layout: post
title: "Implementing video trimming with adjustable aspect ratio in Flutter"
description: " "
date: 2023-10-03
tags: [videotrimming, aspectratio]
comments: true
share: true
---

In this tutorial, we will explore how to implement video trimming with an adjustable aspect ratio in a Flutter application. Video trimming is a useful feature that allows users to select a specific portion of a video for editing or sharing. Additionally, providing the ability to adjust the aspect ratio of the trimmed video can enhance the user experience.

## Prerequisites

To follow along with this tutorial, you should have basic knowledge of Flutter and Dart programming language. Additionally, make sure you have Flutter installed on your machine.

## Dependencies

We'll be using the following dependencies to implement video trimming and adjustable aspect ratio:

- `video_player`: A Flutter plugin for displaying videos.
- `chewie`: A video player plugin for Flutter with customizable UI.
- `flutter_ffmpeg`: A Flutter plugin for executing FFmpeg commands.
- `image_picker`: A Flutter plugin for selecting images and videos from the device gallery.

You can add these dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_player: ^2.3.5
  chewie: ^1.2.2
  flutter_ffmpeg: ^0.4.3
  image_picker: ^0.8.2+3
```

## Implementation

1. Firstly, import the required dependencies in your Flutter project:

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';
import 'package:chewie/chewie.dart';
import 'package:flutter_ffmpeg/flutter_ffmpeg.dart';
import 'package:image_picker/image_picker.dart';
```

2. Define the state for the video player and the chewie controller:

```dart
class VideoTrimmerPage extends StatefulWidget {
  @override
  _VideoTrimmerPageState createState() => _VideoTrimmerPageState();
}

class _VideoTrimmerPageState extends State<VideoTrimmerPage> {
  VideoPlayerController _videoPlayerController;
  ChewieController _chewieController;
  bool _isVideoTrimmed = false;
  double _aspectRatio = 16 / 9;
  // Rest of the code...
}
```

3. Implement the methods to select and play the video:

```dart
Future<void> _pickAndPlayVideo() async {
  final pickedVideo = await ImagePicker().pickVideo(source: ImageSource.gallery);
  if (pickedVideo != null) {
    final videoFile = await pickedVideo.path;
    _videoPlayerController = VideoPlayerController.file(File(videoFile));
    await _videoPlayerController.initialize();
    _chewieController = ChewieController(
      videoPlayerController: _videoPlayerController,
      autoPlay: false,
      looping: false,
    );
    setState(() {});
  }
}

Widget _buildVideoPlayer() {
  if (_chewieController != null && _videoPlayerController.value.isInitialized) {
    return Chewie(controller: _chewieController);
  }
  return CircularProgressIndicator();
}
```

4. Implement the method to trim the video:

```dart
Future<void> _trimVideo() async {
  final directory = await getTemporaryDirectory();
  final outputPath = '${directory.path}/trimmed_video.mp4';
  final ffmpeg = FlutterFFmpeg();
  final arguments = '-y -i ${_videoPlayerController.path} -vf "crop=out_w=${_chewieController.videoPlayerController.value.aspectRatio < _aspectRatio ? _chewieController.videoPlayerController.value.size.height : _chewieController.videoPlayerController.value.size.width}:out_h=${_chewieController.videoPlayerController.value.aspectRatio < _aspectRatio ? _chewieController.videoPlayerController.value.size.height * _aspectRatio : _chewieController.videoPlayerController.value.size.width * _aspectRatio}:out_x=${(_chewieController.videoPlayerController.value.size.width - (_chewieController.videoPlayerController.value.aspectRatio < _aspectRatio ? _chewieController.videoPlayerController.value.size.height : _chewieController.videoPlayerController.value.size.width) * _aspectRatio) / 2}:out_y=0" -c:a copy $outputPath';
  await ffmpeg.execute(arguments);
  final trimmedVideoFile = File(outputPath);
  if (trimmedVideoFile.existsSync()) {
    _videoPlayerController = VideoPlayerController.file(trimmedVideoFile);
    await _videoPlayerController.initialize();
    _chewieController = ChewieController(
      videoPlayerController: _videoPlayerController,
      autoPlay: false,
      looping: false,
    );
    _isVideoTrimmed = true;
    setState(() {});
  }
}
```

5. Finally, implement the UI to display the video player, trimming button, and aspect ratio adjustment controls:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text('Video Trimmer'),
    ),
    body: Center(
      child: Column(
        children: [
          SizedBox(height: 16),
          ElevatedButton(
            onPressed: _pickAndPlayVideo,
            child: Text('Select Video'),
          ),
          SizedBox(height: 16),
          Expanded(child: _buildVideoPlayer()),
          SizedBox(height: 16),
          ElevatedButton(
            onPressed: _isVideoTrimmed ? null : _trimVideo,
            child: Text('Trim Video'),
          ),
          SizedBox(height: 16),
          Slider(
            min: 9 / 16,
            max: 16 / 9,
            value: _aspectRatio,
            onChanged: (newValue) {
              setState(() {
                _aspectRatio = newValue;
              });
            },
          ),
          SizedBox(height: 16),
        ],
      ),
    ),
  );
}
```

That's it! You have successfully implemented video trimming with adjustable aspect ratio in your Flutter application. Users can now select and trim videos, while also adjusting the aspect ratio for their desired output.

Enjoy coding and enhancing your Flutter applications with this useful feature!

#flutter #videotrimming #aspectratio
---
layout: post
title: "Implementing video trimming with simultaneous preview in Flutter"
description: " "
date: 2023-10-03
tags: [videoediting, flutterdevelopment]
comments: true
share: true
---

In this tutorial, we will learn how to implement video trimming with simultaneous preview in a Flutter application. This will allow users to select a portion of a video and see a real-time preview of the trimmed video.

## Prerequisites
Before getting started, make sure you have the following software installed on your machine:
- Flutter SDK
- Android Studio / Xcode (depending on the platform you are developing for)
- Any video editing library (we will be using the `video_player` package in this tutorial)

## Step 1: Set Up the Project
First, create a new Flutter project and add the necessary dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_player: ^2.1.6
```

Run `flutter pub get` to fetch the dependencies.

## Step 2: Build the User Interface
Create a new Dart file, `trim_video_screen.dart`, for the screen where the video trimming will occur. 

In the `TrimVideoScreen` widget, create a video player widget and a draggable range slider widget. The video player will display the selected portion of the video, and the range slider will allow the user to select the trimming start and end points.

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';

class TrimVideoScreen extends StatefulWidget {
  @override
  _TrimVideoScreenState createState() => _TrimVideoScreenState();
}

class _TrimVideoScreenState extends State<TrimVideoScreen> {
  final VideoPlayerController _videoPlayerController =
      VideoPlayerController.asset("assets/sample_video.mp4");
  
  double _startPosition = 0.0;
  double _endPosition = 1.0;
  
  @override
  void initState() {
    super.initState();
    _videoPlayerController.initialize().then((_) {
      setState(() {});
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
        title: Text("Video Trimming"),
      ),
      body: Column(
        children: [
          AspectRatio(
            aspectRatio: _videoPlayerController.value.aspectRatio,
            child: VideoPlayer(_videoPlayerController),
          ),
          RangeSlider(
            values: RangeValues(_startPosition, _endPosition),
            onChanged: (RangeValues values) {
              setState(() {
                _startPosition = values.start;
                _endPosition = values.end;
              });
              _videoPlayerController.seekTo(
                Duration(
                  milliseconds:
                      (_videoPlayerController.value.duration.inMilliseconds *
                              _startPosition)
                          .round(),
                ),
              );
            },
          ),
        ],
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Trim the video and save the trimmed portion
        },
        child: Icon(Icons.save),
      ),
    );
  }
}
```

## Step 3: Add Navigation
In your main Dart file, `main.dart`, set `TrimVideoScreen` as the initial route of the application:

```dart
import 'package:flutter/material.dart';
import 'package:my_app/trim_video_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Video Trimmer',
      initialRoute: '/',
      routes: {
        '/': (context) => TrimVideoScreen(),
      },
    );
  }
}
```

## Step 4: Implement Video Trimming
To actually trim the video and save the trimmed portion, you can use a video editing library like `flutter_ffmpeg`. 

First, add the `flutter_ffmpeg` dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_ffmpeg: ^X.X.X
```

Replace `X.X.X` with the desired version of `flutter_ffmpeg` and then run `flutter pub get` to fetch the dependency.

Inside the `onPressed` handler of the `FloatingActionButton` in `TrimVideoScreen`, you can use `flutter_ffmpeg` to trim the video and save it using the desired output format:

```dart
import 'package:flutter_ffmpeg/flutter_ffmpeg.dart';

// ...
  
void _trimAndSaveVideo() async {
  final FlutterFFmpeg _flutterFFmpeg = FlutterFFmpeg();
  
  final String inputPath = "assets/sample_video.mp4";
  final String outputPath = "path/to/save/trimmed_video.mp4";
  final int startTimestamp = _videoPlayerController.value.duration.inMilliseconds * _startPosition;
  final int endTimestamp = _videoPlayerController.value.duration.inMilliseconds * _endPosition;
  final int duration = endTimestamp - startTimestamp;
  
  final String command = "-y -i $inputPath -ss $startTimestamp -t $duration -async 1 $outputPath";
  
  _flutterFFmpeg.execute(command).then((rc) {
    // Trimming completed, handle success or failure
  });
}

// ...

floatingActionButton: FloatingActionButton(
  onPressed: _trimAndSaveVideo,
  child: Icon(Icons.save),
),

// ...
```

## Conclusion
In this tutorial, we learned how to implement video trimming with simultaneous preview in a Flutter application. By using the `video_player` package and a range slider, we were able to provide users with an interactive way to select and preview a portion of a video. Additionally, by integrating `flutter_ffmpeg`, we demonstrated how to actually trim and save the selected portion of the video.

Remember to make adjustments to the paths, durations, and output formats according to your specific requirements.

#flutter #videoediting #flutterdevelopment
---
layout: post
title: "Applying filters to trimmed videos in Flutter"
description: " "
date: 2023-10-03
tags: [VideoEditing]
comments: true
share: true
---

Flutter is a cross-platform framework that allows developers to build beautiful and functional apps for Android, iOS, web, and desktop using a single codebase. It provides a rich set of features and plugins that make it easy to work with multimedia, including videos.

In this blog post, we will explore how to apply filters to trimmed videos in Flutter using the **video_player** and **flutter_ffmpeg** plugins.

## Getting Started

First, we need to add the necessary dependencies to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_player: ^2.2.3
  flutter_ffmpeg: ^0.4.1
```

After adding the dependencies, run `flutter pub get` to download and link them to your project.

## Trimming a Video

To trim a video, we can use the **video_player** plugin. Assuming you have a video file, let's say `example_video.mp4`, stored locally or fetched from an API, you can use the following code to trim the video:

```dart
import 'package:video_player/video_player.dart';

// ...

late VideoPlayerController _controller;

Future<void> trimVideo() async {
  _controller = VideoPlayerController.asset('assets/example_video.mp4');
  
  await _controller.initialize();
  
  _controller.setLooping(true);
  
  final videoDuration = _controller.value.duration;

  final startDuration = Duration(seconds: 10);
  final endDuration = Duration(seconds: 20);
  
  await _controller.seekTo(startDuration);
  
  _controller.setVolume(0.0);
  _controller.play();
  
  // Wait for the video to reach the end duration
  await Future.delayed(endDuration - startDuration);
  
  _controller.setVolume(1.0);
  await _controller.pause();
  
  final trimmedVideo = await _controller.trim(
    start: startDuration,
    end: endDuration
  );
  
  // Do something with the trimmed video
}

void disposeVideo() {
  _controller.dispose();
}
```

In the above code, we initialize the `VideoPlayerController` with the video file path or asset. We seek to the desired start duration, set the volume to 0.0, and play the video. After waiting for the desired end duration, we pause the video and use the `trim()` method to get the trimmed video.

## Applying Filters to the Trimmed Video

To apply filters to the trimmed video, we can use the **flutter_ffmpeg** plugin, which provides bindings to the FFmpeg library. FFmpeg is a powerful multimedia framework that enables developers to manipulate audio and video files in various ways.

Make sure you have FFmpeg installed on your machine. You can download it from the official website or use a package manager if available for your operating system.

Once FFmpeg is installed, you can apply a filter while encoding the trimmed video using the following code:

```dart
import 'package:flutter_ffmpeg/flutter_ffmpeg.dart';

Future<void> applyFilter() async {
  final ffmpeg = FlutterFFmpeg();

  final inputPath = trimFilePath; // Replace with the path to the trimmed video file
  final outputPath = 'path/to/output_video.mp4'; // Replace with the desired output path

  final filters = 'hue=s=0'; // Example filter: changes the hue of the video

  final command = '-i $inputPath -vf "$filters" $outputPath';

  final int rc = await ffmpeg.execute(command);
  
  if (rc != 0) {
    print('Error applying filter');
    return;
  }

  // You can now use the filtered video as desired
}
```

In the code above, we create an instance of `FlutterFFmpeg`, define input and output paths, specify filters to apply, and build the FFmpeg command using the `-vf` option. Finally, we execute the command using the `execute()` method.

To apply different filters, you can explore the FFmpeg documentation for a wide range of available filters and their parameters.

## Conclusion

In this blog post, we learned how to trim a video using the **video_player** plugin in Flutter and apply filters using the **flutter_ffmpeg** plugin. With these techniques, you can enhance your video editing capabilities and create more dynamic and engaging user experiences in your Flutter apps.

#Flutter #VideoEditing
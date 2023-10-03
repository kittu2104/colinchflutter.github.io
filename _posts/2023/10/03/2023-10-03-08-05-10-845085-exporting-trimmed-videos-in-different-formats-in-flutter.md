---
layout: post
title: "Exporting trimmed videos in different formats in Flutter"
description: " "
date: 2023-10-03
tags: [flutter, video]
comments: true
share: true
---

Flutter, the cross-platform framework developed by Google, provides an easy way to develop mobile applications with native performance. In this blog post, we will learn how to export trimmed videos in different formats using Flutter.

## The problem

Imagine you have a video editing app built with Flutter, and you want to give users the ability to trim and export their videos in different formats like MP4, AVI, or MOV. 

## The solution

To achieve this functionality, we can make use of the `flutter_ffmpeg` package available on pub.dev. This package wraps the FFmpeg command-line tool and allows us to process videos directly from our Flutter application.

### Steps

1. To get started, follow the installation instructions for the `flutter_ffmpeg` package mentioned in the package's documentation on pub.dev.

2. Once you have added the package to your Flutter project, import it into your Dart file:

```dart
import 'package:flutter_ffmpeg/flutter_ffmpeg.dart';
```

3. Next, create an instance of the `FlutterFFmpeg` class:

```dart
final FlutterFFmpeg _flutterFFmpeg = FlutterFFmpeg();
```

4. To trim the video, use the following code snippet:

```dart
String inputFilePath = '/path/to/input/video.mp4';
String outputFilePath = '/path/to/output/trimmed_video.mp4';
String startDuration = '00:00:05'; // Start time of the trimmed video
String endDuration = '00:00:15'; // End time of the trimmed video

String trimCommand = '-i $inputFilePath -ss $startDuration -to $endDuration -c copy $outputFilePath';

await _flutterFFmpeg.execute(trimCommand);
```
In the above code, we provide the input file path, output file path, start duration, and end duration in the `trimCommand` string. The `execute` method runs the FFmpeg command to trim the video.

5. Finally, to export the video in different formats, simply change the output file extension in the `outputFilePath` string to the desired format (e.g., `.avi` or `.mov`).

By following these steps, you can now trim and export videos in different formats in your Flutter application.

## Conclusion

In this blog post, we learned how to use the `flutter_ffmpeg` package to export trimmed videos in different formats using Flutter. With this functionality integrated into your app, users can effortlessly edit and share their videos in various file formats. 

#flutter #video-processing
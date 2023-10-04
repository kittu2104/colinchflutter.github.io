---
layout: post
title: "Adding text overlays to trimmed videos in Flutter"
description: " "
date: 2023-10-03
tags: [videoplayer, videoediting]
comments: true
share: true
---

In this tutorial, we will learn how to add text overlays to trimmed videos in Flutter using the video_player and video_editing libraries. We will first trim a video using the video_editing library and then add text overlays on top of the trimmed video using the video_player library.

## Prerequisites

Before we get started, make sure you have Flutter and the video_player and video_editing libraries installed. You can add the video_player and video_editing dependencies to your pubspec.yaml file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_player: ^0.11.0
  video_editing: ^0.4.0
```

Then, import the necessary packages in your Dart file:
```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';
import 'package:video_editing/video_editing.dart';
```

## Trimming a Video

First, we need to trim the video using the video_editing library. We will create a function called `trimVideo` that takes in the sourcePath (path of the original video), startTime, and endTime to trim the video.

```dart
Future<String> trimVideo(String sourcePath, int startTime, int endTime) async {
  final input = MediaInfo(
    sourcePath: sourcePath,
  );

  final trim = Trim(
    startTime: Duration(milliseconds: startTime),
    duration: Duration(milliseconds: endTime - startTime),
  );

  final output = OutputFile(
    outputFile: 'trimmedVideo.mp4',
    formatHint: OutputFormat.mp4,
  );

  final job = Job(
    input: input,
    edits: [trim],
    output: output,
  );

  final executor = JobExecutor();

  final result = await executor.execute(job);
  if (result.status == JobStatus.success) {
    return result.outputFile.path;
  } else {
    throw Exception('Failed to trim video');
  }
}
```

## Adding Text Overlay to Trimmed Video

Once we have trimmed the video, we can add a text overlay to it. We will create a function called `addTextOverlay` that takes in the path of the trimmed video and the text content.

```dart
void addTextOverlay(String videoPath, String text) {
  final videoPlayerController = VideoPlayerController.file(File(videoPath));
  final initialize = videoPlayerController.initialize(); // Initialize the video player controller

  initialize.then((_) {
    final videoPlayer = videoPlayerController.value;

    final width = videoPlayer.size.width.toInt();
    final height = videoPlayer.size.height.toInt();

    final textPainter = TextPainter(
      text: TextSpan(
        text: text,
        style: TextStyle(
          fontSize: 24,
          color: Colors.white,
          fontWeight: FontWeight.bold,
        ),
      ),
      textDirection: TextDirection.ltr,
    );

    textPainter.layout(maxWidth: width.toDouble());

    final xPos = (width / 2) - (textPainter.width / 2);
    final yPos = height - textPainter.height - 16;

    final videoOverlay = Overlay(
      x: xPos.toInt(),
      y: yPos.toInt(),
      width: textPainter.width.toInt(),
      height: textPainter.height.toInt(),
      child: Text(text),
      textStyle: TextStyle(
        fontSize: 24,
        color: Colors.white,
        fontWeight: FontWeight.bold,
      ),
    );

    final videoEditorController = VideoEditorController(videoPath)
      ..initialize().then((_) {
        videoEditorController.addOverlay(videoOverlay);

        final outputPath = 'videoWithText.mp4';
        videoEditorController.export(outputPath);

        videoEditorController.dispose();
      });
  });
}
```

## Conclusion

In this tutorial, we have learned how to add text overlays to trimmed videos in Flutter using the video_player and video_editing libraries. We first trimmed the video using the video_editing library and then added text overlays on top of the trimmed video using the video_player library. With these techniques, you can easily customize and enhance your video editing experience in your Flutter applications.

#flutter #videoplayer #videoediting
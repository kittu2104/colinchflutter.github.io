---
layout: post
title: "Adding custom video thumbnail selection during trimming in Flutter"
description: " "
date: 2023-10-03
tags: []
comments: true
share: true
---

If you are working on a Flutter project that involves video editing or video trimming functionality, you may want to provide the user with the ability to select a custom thumbnail for their video. By default, when trimming a video, the platform often selects a random frame from the video as the thumbnail. However, allowing the user to choose a specific frame as the thumbnail can enhance the user experience and make the video more enticing. In this blog post, we will explore how to add custom video thumbnail selection during trimming in Flutter.


## Prerequisites

Before we get started, make sure you have the following prerequisites installed:

- Flutter SDK
- Flutter IDE (such as Android Studio or Visual Studio Code)

## Getting Started

To begin, create a new Flutter project by running the following command:

```dart
flutter create custom_thumbnail_selection
cd custom_thumbnail_selection
```

## Adding the Video Trimming Functionality

To add video trimming functionality to your Flutter app, you can use the `video_trimmer` package. This package provides an easy way to trim videos in Flutter. Add the package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_trimmer: ^2.2.0
```

Run `flutter pub get` to fetch the package.

## Implementing Custom Video Thumbnail Selection

To add custom video thumbnail selection during trimming, we can use the `video_thumbnail` package. It allows us to extract a thumbnail from a specific frame of the video using its timestamp. Add the package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_thumbnail: ^2.1.0
```

Run `flutter pub get` to fetch the package.

## Selecting a Custom Thumbnail

To allow the user to select a custom thumbnail, you can display a list of frames from the trimmed video and let the user choose one. You can use a `ListView` widget to display the frames as a scrollable list. Use the `video_thumbnail` package to generate thumbnails for each frame.

Here's an example code snippet demonstrating how you can display a list of thumbnails:

```dart
import 'package:flutter/material.dart';
import 'package:video_trimmer/video_trimmer.dart';
import 'package:video_thumbnail/video_thumbnail.dart';

class CustomThumbnailSelection extends StatefulWidget {
  final Trimmer _trimmer;

  CustomThumbnailSelection(this._trimmer);

  @override
  _CustomThumbnailSelectionState createState() =>
      _CustomThumbnailSelectionState();
}

class _CustomThumbnailSelectionState extends State<CustomThumbnailSelection> {
  List<Widget> thumbnails = [];

  @override
  void initState() {
    super.initState();
    generateThumbnails();
  }

  void generateThumbnails() async {
    final videoFile = await widget._trimmer.getTrimmedVideo();
    final numberOfThumbnails = 5;
    final duration = widget._trimmer.videoDuration;

    double frameDuration = duration / numberOfThumbnails;

    for (int i = 0; i < numberOfThumbnails; i++) {
      final thumbnail = await VideoThumbnail.thumbnailData(
        video: videoFile.path,
        imageFormat: ImageFormat.JPEG,
        timeMs: (i * frameDuration).toInt(),
      );

      setState(() {
        thumbnails.add(
          Image.memory(thumbnail),
        );
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return ListView(
      scrollDirection: Axis.horizontal,
      children: thumbnails,
    );
  }
}
```

In this example, we generate multiple thumbnails using the `VideoThumbnail.thumbnailData` method from the `video_thumbnail` package. We then add the thumbnails to the `ListView` widget to display them horizontally. You can customize the number of thumbnails and the duration between them according to your app requirements.


## Conclusion

In this blog post, we learned how to add custom video thumbnail selection during video trimming in a Flutter app. By allowing the user to choose a specific frame as the thumbnail, you can enhance the user experience and make the video more appealing.
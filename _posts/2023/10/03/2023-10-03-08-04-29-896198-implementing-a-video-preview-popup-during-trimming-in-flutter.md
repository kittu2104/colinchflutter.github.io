---
layout: post
title: "Implementing a video preview popup during trimming in Flutter"
description: " "
date: 2023-10-03
tags: [flutter, videoTrimming, popup]
comments: true
share: true
---

## Introduction

In this tutorial, we will learn how to implement a video preview popup during the trimming process in a Flutter application. This feature allows users to preview the video before finalizing the trim selection.

## Prerequisites

To follow along with this tutorial, you should have a basic understanding of Flutter and have Flutter SDK installed on your machine. You will also need a code editor, such as Visual Studio Code or Android Studio, to write and run the Flutter code.

## Step 1: Add Required Dependencies

We will need to add two dependencies to our `pubspec.yaml` file. Open the file and add the following lines:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_player: ^2.2.3
  chewie: ^1.1.1
```

The `video_player` package provides video playback functionality, and the `chewie` package simplifies the integration of the video_player with UI elements.

Save the `pubspec.yaml` file and run the `flutter pub get` command in the terminal to fetch the dependencies.

## Step 2: Create Video Trimming Page

Create a new Dart file called `video_trimming_page.dart`. Import the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';
import 'package:chewie/chewie.dart';
```

Create a stateful widget class called `VideoTrimmingPage`:

```dart
class VideoTrimmingPage extends StatefulWidget {
  @override
  _VideoTrimmingPageState createState() => _VideoTrimmingPageState();
}
```

Add a `_videoPlayerController` and a `_chewieController` as class variables:

```dart
class _VideoTrimmingPageState extends State<VideoTrimmingPage> {
  VideoPlayerController _videoPlayerController;
  ChewieController _chewieController;
}
```

In the `initState` method, initialize the video player and chewie controller:

```dart
@override
void initState() {
  super.initState();
  _videoPlayerController = VideoPlayerController.network('https://example.com/video.mp4');
  _chewieController = ChewieController(
    videoPlayerController: _videoPlayerController,
    autoPlay: false,
    looping: false,
    allowFullScreen: false,
  );
}
```

Override the `dispose` method to dispose the video player and chewie controller when the page is disposed:

```dart
@override
void dispose() {
  super.dispose();
  _videoPlayerController.dispose();
  _chewieController.dispose();
}
```

Implement the build method to return the UI elements:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text('Video Trimming'),
    ),
    body: Center(
      child: Chewie(
        controller: _chewieController,
      ),
    ),
  );
}
```

## Step 3: Show Video Preview Popup

To show the video preview popup, we will use a `showModalBottomSheet` method, which displays a bottom sheet modal. Modify the build method as follows:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text('Video Trimming'),
    ),
    body: Center(
      child: ElevatedButton(
        onPressed: () {
          showModalBottomSheet(
            context: context,
            builder: (context) {
              return Container(
                height: 300,
                child: Column(
                  children: [
                    Chewie(
                      controller: _chewieController,
                    ),
                    ElevatedButton(
                      onPressed: () {
                        Navigator.of(context).pop();
                        // Perform additional action after preview
                      },
                      child: Text('Select'),
                    ),
                  ],
                ),
              );
            },
          );
        },
        child: Text('Preview'),
      ),
    ),
  );
}
```

In the above code, we added an `ElevatedButton` with an `onPressed` callback. Inside the callback, we use the `showModalBottomSheet` method to show a modal sheet containing a `Chewie` widget for video preview. The `ElevatedButton` with the 'Select' label allows users to finalize the trim selection and perform any additional actions after the preview.

## Conclusion

In this tutorial, we learned how to implement a video preview popup during the trimming process in a Flutter application. By using the `video_player` and `chewie` packages, we were able to easily integrate video playback and UI elements. This feature enhances user experience and provides a better understanding of the final trim selection.

#flutter #videoTrimming #popup
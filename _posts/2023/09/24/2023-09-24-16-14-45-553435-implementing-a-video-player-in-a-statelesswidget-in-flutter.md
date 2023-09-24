---
layout: post
title: "Implementing a video player in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [flutter, videoplayer]
comments: true
share: true
---

Flutter, a popular cross-platform framework developed by Google, provides an easy way to implement a video player in your app. In this tutorial, we will show you how to create a video player using Flutter's StatelessWidget.

### Step 1: Adding Dependencies

The first step is to add the necessary dependencies to your `pubspec.yaml` file. Open the file and add the following lines:

```yaml
dependencies:
  flutter:
    sdk: flutter

  video_player: ^2.2.5
```

Save the file and run `flutter pub get` in your terminal to fetch the dependencies.

### Step 2: Creating a Video Player

Next, we will create a new file called `video_player_widget.dart` and define our `VideoPlayerWidget` class. Here's an example implementation:

```dart
import 'package:flutter/material.dart';
import 'package:video_player/video_player.dart';

class VideoPlayerWidget extends StatelessWidget {
  final String videoUrl;
  final VideoPlayerController controller;

  VideoPlayerWidget({required this.videoUrl})
      : controller = VideoPlayerController.network(videoUrl);

  @override
  Widget build(BuildContext context) {
    return AspectRatio(
      aspectRatio: 16 / 9, // Adjust according to your video's aspect ratio
      child: Container(
        child: VideoPlayer(controller),
      ),
    );
  }
}
```

In the `VideoPlayerWidget` class, we define two properties: `videoUrl` for the URL of the video and `controller` to control the video playback. We initialize the `controller` using `VideoPlayerController.network()` and pass the `videoUrl` as a parameter.

Within the `build()` method, we return an `AspectRatio` widget that maintains the aspect ratio of the video, and a `Container` with a child `VideoPlayer` widget.

### Step 3: Using the Video Player Widget

Now that we have our `VideoPlayerWidget`, let's use it in another part of our app. For example, we can add it to a `Scaffold` widget in the `build()` method of a stateful or stateless widget.

```dart
import 'package:flutter/material.dart';
import 'video_player_widget.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Video Player Example')),
        body: Center(
          child: VideoPlayerWidget(videoUrl: 'https://example.com/video.mp4'),
        ),
      ),
    );
  }
}

void main() {
  runApp(MyApp());
}
```

In the above example, we import the `VideoPlayerWidget` and then use it as a child of the `Center` widget in the `body` of our `Scaffold`. We pass the `videoUrl` as a parameter to the `VideoPlayerWidget`.

### Conclusion

In this tutorial, we learned how to implement a video player using a `StatelessWidget` in Flutter. It's important to note that this implementation uses the `video_player` package to handle video playback. You can customize the video player and add additional functionalities according to your app's requirements.

#flutter #videoplayer
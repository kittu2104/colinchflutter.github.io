---
layout: post
title: "Adding video rotation and flipping during trimming in Flutter"
description: " "
date: 2023-10-03
tags: [VideoEditing]
comments: true
share: true
---

Flutter is a popular cross-platform framework that allows developers to build beautiful and efficient mobile applications. With its rich set of libraries and plugins, it offers a wide range of functionalities for developers to implement in their applications. In this blog post, we will explore how to add video rotation and flipping during trimming in a Flutter application.

## Why Video Rotation and Flipping?

Video rotation and flipping are commonly used features in video editing applications. They allow users to adjust the orientation and flip the video to get the desired effect. Adding these features can enhance the overall experience of the application and provide more control to the users.

## Implementing Video Rotation and Flipping

To implement video rotation and flipping during trimming in a Flutter application, we can make use of the `video_player` and `transformer_page_view` plugins. These plugins provide the necessary functionalities to play videos and apply transformations.

### Step 1: Setup Dependencies

First, we need to add the required dependencies to the `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  video_player: ^2.2.5
  transformer_page_view: ^1.0.2
```

After adding the dependencies, run `flutter pub get` to download and install them in your project.

### Step 2: Playing and Trimming the Video

To play and trim the video, we can use the `video_player` plugin. Create a new Flutter widget and wrap it with the `VideoPlayerController` widget. Set the video source and initialize the controller:

```dart
import 'package:video_player/video_player.dart';

class VideoPlayerWidget extends StatefulWidget {
  final String videoUrl;

  const VideoPlayerWidget({Key key, this.videoUrl}) : super(key: key);

  @override
  _VideoPlayerWidgetState createState() => _VideoPlayerWidgetState();
}

class _VideoPlayerWidgetState extends State<VideoPlayerWidget> {
  VideoPlayerController _controller;

  @override
  void initState() {
    super.initState();
    _controller = VideoPlayerController.network(widget.videoUrl)
      ..initialize().then((_) {
        setState(() {});
      });
  }

  @override
  void dispose() {
    super.dispose();
    _controller.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return _controller.value.isInitialized
        ? AspectRatio(
            aspectRatio: _controller.value.aspectRatio,
            child: VideoPlayer(_controller),
          )
        : Container();
  }
}
```

You can now use this widget to play the video by passing the video URL to the `videoUrl` parameter.

### Step 3: Applying Transformation

To apply rotation and flipping to the video, we can use the `transformer_page_view` plugin. Wrap the `VideoPlayerWidget` inside the `TransformerPageView` widget, and apply the desired transformations using the `TransformInfo.custom` property:

```dart
import 'package:transformer_page_view/transformer_page_view.dart';

class VideoEditorPage extends StatefulWidget {
  final String videoUrl;

  const VideoEditorPage({Key key, this.videoUrl}) : super(key: key);

  @override
  _VideoEditorPageState createState() => _VideoEditorPageState();
}

class _VideoEditorPageState extends State<VideoEditorPage> {
  PageController _pageController;
  double _rotation = 0.0;
  bool _isFlipped = false;

  @override
  void initState() {
    super.initState();
    _pageController = PageController();
  }

  @override
  void dispose() {
    super.dispose();
    _pageController.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Video Editor'),
      ),
      body: TransformerPageView(
        scrollDirection: Axis.vertical,
        transformer: ScaleAndFadeTransformer(),
        viewportFraction: 0.8,
        physics: ClampingScrollPhysics(),
        controller: _pageController,
        itemCount: 2,
        itemBuilder: (BuildContext context, int index) {
          if (index == 0) {
            return VideoPlayerWidget(
              videoUrl: widget.videoUrl,
            );
          } else {
            return CustomTransformWidget(
              child: VideoPlayerWidget(
                videoUrl: widget.videoUrl,
              ),
              rotation: _rotation,
              flipHorizontal: _isFlipped,
              onRotationChanged: (double value) {
                setState(() {
                  _rotation = value;
                });
              },
              onFlipChanged: (bool value) {
                setState(() {
                  _isFlipped = value;
                });
              },
            );
          }
        },
      ),
    );
  }
}
```

In the above implementation, `CustomTransformWidget` is a custom widget that applies the rotation and flipping transformations to its child widget. It provides callbacks `onRotationChanged` and `onFlipChanged` to update the rotation and flip states.

### Step 4: Testing and Deployment

You can now test the application by running it on a device or emulator. Make sure to test different video formats and ensure that the rotation and flipping features work as expected. Once you are satisfied with the functionality, you can proceed with deploying the application.

## Conclusion

In this blog post, we have seen how to add video rotation and flipping during trimming in a Flutter application. By utilizing the `video_player` and `transformer_page_view` plugins, we were able to play videos and apply transformations dynamically. This functionality can be extended to implement more advanced video editing features in Flutter applications. Happy coding!

\#Flutter \#VideoEditing
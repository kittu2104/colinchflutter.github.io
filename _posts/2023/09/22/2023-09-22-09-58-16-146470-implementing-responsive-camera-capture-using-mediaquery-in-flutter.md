---
layout: post
title: "Implementing responsive camera capture using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [Flutter, ResponsiveDesign]
comments: true
share: true
---

![Flutter](https://flutter.dev/images/flutter-logo-sharing.png)

In this blog post, I will walk you through the process of implementing a responsive camera capture feature in a Flutter application using the `MediaQuery` class. This will allow your application to adapt to different screen sizes and orientations, ensuring a seamless user experience on various devices.

## What is MediaQuery?

`MediaQuery` is a Flutter class that provides information about the current device's size, orientation, and other characteristics. By leveraging the `MediaQuery` class, we can adjust the layout of our widgets dynamically based on the available screen real estate.

## Setting Up the Camera Capture Widget

First, we need to set up the camera capture widget. We will be using the `camera` package in Flutter to handle the camera functionality. 

```dart
import 'dart:async';
import 'package:camera/camera.dart';
import 'package:flutter/material.dart';

class CameraCaptureWidget extends StatefulWidget {
  @override
  _CameraCaptureWidgetState createState() => _CameraCaptureWidgetState();
}

class _CameraCaptureWidgetState extends State<CameraCaptureWidget> {
  CameraController _cameraController;
  Future<void> _initializeControllerFuture;

  @override
  void initState() {
    super.initState();
    _setUpCamera();
  }

  void _setUpCamera() async {
    final cameras = await availableCameras();
    final firstCamera = cameras.first;

    _cameraController = CameraController(
      firstCamera,
      ResolutionPreset.medium,
    );

    _initializeControllerFuture = _cameraController.initialize();
  }

  @override
  void dispose() {
    _cameraController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return FutureBuilder<void>(
      future: _initializeControllerFuture,
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.done) {
          return _cameraPreviewWidget();
        } else {
          return Center(child: CircularProgressIndicator());
        }
      },
    );
  }

  Widget _cameraPreviewWidget() {
    final mediaQuery = MediaQuery.of(context);
    final cameraAspect =
        _cameraController.value.aspectRatio ?? mediaQuery.size.aspectRatio;

    return AspectRatio(
      aspectRatio: cameraAspect,
      child: CameraPreview(_cameraController),
    );
  }
}
```

In the above code, we create a `CameraCaptureWidget` that handles the camera functionality. We use the `camera` package to set up the camera controller, initialize it, and show the camera preview using the `CameraPreview` widget. The `AspectRatio` widget ensures that the camera preview maintains its aspect ratio.

## Making the Camera Capture Responsive

To make the camera capture widget responsive, we can leverage the properties provided by the `MediaQuery` class. Let's modify our `_cameraPreviewWidget` method to dynamically adjust the aspect ratio based on the available screen real estate.

```dart
  Widget _cameraPreviewWidget() {
    final mediaQuery = MediaQuery.of(context);
    final cameraAspect =
        _cameraController.value.aspectRatio ?? mediaQuery.size.aspectRatio;

    if (mediaQuery.orientation == Orientation.portrait) {
      return AspectRatio(
        aspectRatio: cameraAspect,
        child: CameraPreview(_cameraController),
      );
    } else {
      return SizedBox(
        width: mediaQuery.size.width,
        child: AspectRatio(
          aspectRatio: cameraAspect,
          child: CameraPreview(_cameraController),
        ),
      );
    }
  }
```

In the modified code, if the device is in portrait orientation, we use `AspectRatio` to ensure the camera preview maintains its desired aspect ratio. However, if the device is in landscape orientation, we wrap the `AspectRatio` inside a `SizedBox` widget to make it occupy the full width of the screen.

Now, when users rotate their device or switch between portrait and landscape mode, the camera capture widget will respond dynamically and adapt its layout accordingly.

## Conclusion

By using the `MediaQuery` class in Flutter, we can easily implement a responsive camera capture feature in our application. This enables our app to seamlessly adjust its UI based on the device's screen size and orientation, providing a consistent and optimal user experience.

Start implementing responsive camera capture in your Flutter applications and enhance the user experience across different devices.

### #Flutter #ResponsiveDesign
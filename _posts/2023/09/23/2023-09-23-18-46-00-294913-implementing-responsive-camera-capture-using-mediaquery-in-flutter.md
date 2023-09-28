---
layout: post
title: "Implementing responsive camera capture using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [CameraCapture]
comments: true
share: true
---

In today's mobile app development, having a responsive camera capture feature is essential for capturing images in different device orientations and screen sizes. In this tutorial, we'll learn how to implement a responsive camera capture using the `MediaQuery` class in Flutter.

## Step 1: Set up the project

Create a new Flutter project and open the main.dart file. In the dependencies section of the pubspec.yaml file, add the `camera` and `path_provider` plugins.

```yaml
dependencies:
  flutter:
    sdk: flutter
  camera: ^0.9.4
  path_provider: ^2.0.2
```

Make sure to run `flutter pub get` to download the required plugins.

## Step 2: Create the camera screen

Create a new file called `camera_screen.dart`. Inside this file, define a stateful widget called `CameraScreen`. This widget will be responsible for displaying the camera preview and capturing the image.

```dart
import 'package:flutter/material.dart';
import 'package:camera/camera.dart';

class CameraScreen extends StatefulWidget {
  @override
  _CameraScreenState createState() => _CameraScreenState();
}

class _CameraScreenState extends State<CameraScreen> {
  CameraController _controller;
  Future<void> _initializeControllerFuture;

  @override
  void initState() {
    super.initState();
    _initializeCamera();
  }

  Future<void> _initializeCamera() async {
    final cameras = await availableCameras();
    _controller = CameraController(cameras[0], ResolutionPreset.medium);
    _initializeControllerFuture = _controller.initialize();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Camera Capture'),
      ),
      body: FutureBuilder<void>(
        future: _initializeControllerFuture,
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.done) {
            return CameraPreview(_controller);
          } else {
            return Center(child: CircularProgressIndicator());
          }
        },
      ),
      floatingActionButton: FloatingActionButton(
        child: Icon(Icons.camera),
        onPressed: () {
          _captureImage();
        },
      ),
    );
  }

  Future<void> _captureImage() async {
    if (_controller.value.isInitialized) {
      final directory = await getTemporaryDirectory();
      final path = '${directory.path}/image.png';
      await _controller.takePicture(path);
    }
  }
}
```

In the `_initializeCamera` method, we use the `camera` plugin to retrieve the list of available cameras and initialize the controller with the first camera. In the `build` method, a `CameraPreview` widget is used to display the live camera preview. The `_captureImage` method is called when the user taps on the floating action button to capture the image.

## Step 3: Implement responsive camera capture

To make the camera capture responsive, we can use the `MediaQuery` class to get the screen dimensions and adjust the camera preview size accordingly.

Inside the `_CameraScreenState` class, add the following method:

```dart
Future<void> _adjustCameraPreviewSize() async {
  if (_controller.value.isInitialized) {
    final screenSize = MediaQuery.of(context).size;
    final screenRatio = screenSize.aspectRatio;

    final previewSize = _controller.value.previewSize;
    final previewRatio = previewSize.height / previewSize.width;

    if (screenRatio > previewRatio) {
      setState(() {
        _controller.setPreviewSize(
          Size(previewSize.height / screenRatio, previewSize.height),
        );
      });
    } else {
      setState(() {
        _controller.setPreviewSize(
          Size(previewSize.width, previewSize.width * screenRatio),
        );
      });
    }
  }
}
```

This method calculates the screen aspect ratio and compares it with the camera preview aspect ratio. If the screen ratio is greater, it means the screen is more vertical, and we need to adjust the preview size accordingly. The `_adjustCameraPreviewSize` method is then called in the `_initializeCamera` method and after device orientation changes:

```dart
Future<void> _initializeCamera() async {
  final cameras = await availableCameras();
  _controller = CameraController(cameras[0], ResolutionPreset.medium);
  _initializeControllerFuture = _controller.initialize();
  _adjustCameraPreviewSize();
}

@override
void didChangeDependencies() {
  super.didChangeDependencies();
  _adjustCameraPreviewSize();
}
```

## Step 4: Usage example

To use the `CameraScreen` widget in your app, you can simply create a new route and push it onto the navigator stack. For example:

```dart
MaterialApp(
  home: Scaffold(
    appBar: AppBar(
      title: Text('My App'),
    ),
    body: Center(
      child: ElevatedButton(
        child: Text('Take Picture'),
        onPressed: () {
          Navigator.push(
            context,
            MaterialPageRoute(builder: (context) => CameraScreen()),
          );
        },
      ),
    ),
  ),
);
```

## Conclusion

In this tutorial, we learned how to implement a responsive camera capture feature using the `MediaQuery` class in Flutter. By using the screen dimensions and camera preview size, we can adjust the camera view to fit different device orientations and screen sizes. This allows users to capture images seamlessly regardless of the device they are using.

#Flutter #CameraCapture
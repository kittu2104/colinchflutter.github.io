---
layout: post
title: "Implementing real-time image processing using Flutter camera"
description: " "
date: 2023-09-29
tags: [imageProcessing]
comments: true
share: true
---

In this blog post, we will explore how to implement real-time image processing using the Flutter Camera package. Flutter is a popular cross-platform development framework that allows you to build beautiful and native applications for iOS and Android using a single codebase.

To get started, make sure you have Flutter installed on your development machine. You can check the official Flutter documentation for installation instructions.

## Installing the Camera package

First, you need to add the `camera` package as a dependency in your `pubspec.yaml` file:

```dart
dependencies:
  flutter:
    sdk: flutter
  camera: ^0.8.1+3
```

After updating the `pubspec.yaml` file, run the following command in your terminal to fetch the package:

```bash
flutter pub get
```

## Setting up the Camera

To use the device camera in Flutter, we need to add the necessary permissions in the Android and iOS manifests. For Android, open the `AndroidManifest.xml` file located at `android/app/src/main` and add the following permissions:

```xml
<uses-permission android:name="android.permission.CAMERA"/>
<uses-feature android:name="android.hardware.camera" android:required="true"/>
```

For iOS, open the `Info.plist` file located at `ios/Runner` and add the following key-value pairs:

```xml
<key>NSCameraUsageDescription</key>
<string>Your description here (Ex: Camera permission is required for image processing)</string>
```

## Accessing the Camera Stream

Now, let's create a new Flutter widget that will display the camera stream:

```dart
import 'dart:io';
import 'package:flutter/material.dart';
import 'package:camera/camera.dart';

class CameraScreen extends StatefulWidget {
  @override
  _CameraScreenState createState() => _CameraScreenState();
}

class _CameraScreenState extends State<CameraScreen> {
  late CameraController _controller;
  List<CameraDescription> _cameras = [];

  @override
  void initState() {
    super.initState();
    _initializeCamera();
  }

  Future<void> _initializeCamera() async {
    final cameras = await availableCameras();
    setState(() {
      _cameras = cameras;
      _controller = CameraController(cameras[0], ResolutionPreset.high);
      _controller.initialize().then((_) {
        if (!mounted) {
          return;
        }
        setState(() {});
      });
    });
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    if (!_controller.value.isInitialized) {
      return Container(); // Or show a loading indicator
    }
    return Scaffold(
      body: CameraPreview(_controller),
    );
  }
}
```

The `CameraScreen` widget above sets up the camera controller, initializes the camera, and displays the camera preview.

## Implementing Real-Time Image Processing

To implement real-time image processing, we can use the `camera` and `image` packages together. The `image` package provides utilities for image processing, while the `camera` package allows us to capture and display the camera stream.

Let's add a simple image filter that converts the camera stream to grayscale:

```dart
import 'dart:async';
import 'package:flutter/material.dart';
import 'package:camera/camera.dart';
import 'package:image/image.dart' as img;
import 'package:image/image.dart';

class CameraScreen extends StatefulWidget {
  // ... Rest of the code

  Future<Uint8List?> _convertToGrayscale(CameraImage image) async {
    final convertedImage = img.copyResize(
      img.Image.fromBytes(
        image.planes[0].bytesPerRow,
        image.height,
        image.planes[0].bytes,
        format: img.Format.raw,
      ),
      width: image.width,
      height: image.height,
    );
    img.grayscale(convertedImage); // Convert image to grayscale
    return Uint8List.fromList(
      img.encodeJpg(convertedImage),
    );
  }

  void _startImageProcessing() {
    Timer.periodic(Duration(milliseconds: 250), (_) {
      if (_controller?.value.isInitialized != true) {
        return;
      }
      final image = _controller!.takePicture().then(
        (XFile? file) async {
          if (file != null) {
            final bytes = await file.readAsBytes();
            final cameraImage = await CameraImage.fromBytes(
              bytes,
              _controller!.value.previewSize!.width.toInt(),
              _controller!.value.previewSize!.height.toInt(),
              format: ImageFormat.yuv420,
            );
            final grayscaleImage = await _convertToGrayscale(cameraImage);
            // Process the grayscale image here
          }
        },
      );
    });
  }

  @override
  Widget build(BuildContext context) {
    // .. Rest of the code

    _startImageProcessing(); // Start image processing

    return Scaffold(
      body: CameraPreview(_controller),
    );
  }
}
```

In the `_startImageProcessing` method, we set a timer to capture the camera image every 250 milliseconds. We then convert the captured image to grayscale using the `image` package and process the grayscale image as needed.

## Conclusion

In this blog post, we have explored how to implement real-time image processing using Flutter and the Camera package. We covered setting up the camera, accessing the camera stream, and implementing simple image filtering.

Flutter provides a rich set of packages and libraries that make implementing real-time image processing a breeze. As always, it's important to keep in mind the performance implications of image processing and optimize your code accordingly.

Happy coding!

#flutter #imageProcessing
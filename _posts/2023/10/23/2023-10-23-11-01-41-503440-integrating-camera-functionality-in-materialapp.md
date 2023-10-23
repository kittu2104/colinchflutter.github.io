---
layout: post
title: "Integrating camera functionality in MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Many mobile applications require camera functionality to provide users with the ability to capture and work with images. In this tech blog post, we will explore how to integrate camera functionality in a Flutter application using the `camera` package within a MaterialApp widget.

## Table of Contents
- [Setting Up the Project](#setting-up-the-project)
- [Installing the camera Package](#installing-the-camera-package)
- [Granting Camera Permissions](#granting-camera-permissions)
- [Implementing Camera Functionality](#implementing-camera-functionality)
- [Displaying Captured Image](#displaying-captured-image)
- [Conclusion](#conclusion)

## Setting Up the Project

To begin, create a new Flutter project and open it in your preferred code editor. Inside the `lib` directory, open the `main.dart` file.

## Installing the camera Package

Add the `camera` package as a dependency in the `pubspec.yaml` file of your project. This package allows us to interact with the device's camera.

```yaml
dependencies:
  flutter:
    sdk: flutter
  camera: ^0.7.0
```

Run `flutter pub get` to fetch and install the package in your project.

## Granting Camera Permissions

To access the camera, we need to add camera permissions to the `AndroidManifest.xml` file for Android and the `Info.plist` file for iOS. Make sure you've added the necessary permissions and descriptions according to the platform-specific guidelines.

## Implementing Camera Functionality

Inside the `main.dart` file, import the necessary packages:

```dart
import 'package:camera/camera.dart';
```

Next, initialize the camera by creating a `CameraController` instance in the `initState()` method of the widget:

```dart
List<CameraDescription>? cameras;
CameraController? controller;
Future<void>? cameraInitialized;

@override
void initState() {
  super.initState();
  
  // Retrieve the list of available cameras
  cameraInitialized = initializeCamera();
}

Future<void> initializeCamera() async {
  cameras = await availableCameras();

  // Select the first camera from the list
  controller = CameraController(cameras![0], ResolutionPreset.medium);

  // Initialize the camera controller
  await controller!.initialize();
}
```

Once the camera is initialized, we can use the `CameraPreview` widget to display the live camera feed. Add the following code inside the `build` method:

```dart
@override
Widget build(BuildContext context) {
  if (controller == null || !controller!.value.isInitialized) {
    return Container();
  }

  return AspectRatio(
    aspectRatio: controller!.value.aspectRatio,
    child: CameraPreview(controller!),
  );
}
```

## Displaying Captured Image

To capture an image, add a button to your UI and call the `takePicture()` method of the `CameraController`:

```dart
late XFile capturedImage;

void takePicture() async {
  try {
    capturedImage = await controller!.takePicture();

    // Do something with the captured image
  } catch (e) {
    print('Error capturing image: $e');
  }
}
```

After capturing an image, you can display it on the screen using the `Image.file` widget:

```dart
Widget build(BuildContext context) {
  // ...

  return Column(
    children: [
      // Camera preview widget
      AspectRatio(
        aspectRatio: controller!.value.aspectRatio,
        child: CameraPreview(controller!),
      ),
      // Capture button
      ElevatedButton(
        onPressed: takePicture,
        child: Text('Capture'),
      ),
      // Display captured image
      if(capturedImage != null)
        Image.file(File(capturedImage.path)),
    ],
  );
}
```

## Conclusion

By following these steps, you can integrate camera functionality into your MaterialApp Flutter application. Users will now be able to capture images and interact with them within your app. Feel free to customize the UI and add additional features to enhance the camera experience.

Happy coding! 📷🚀
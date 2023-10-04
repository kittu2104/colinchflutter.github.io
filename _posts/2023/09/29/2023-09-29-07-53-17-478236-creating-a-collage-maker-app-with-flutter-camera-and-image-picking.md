---
layout: post
title: "Creating a collage maker app with Flutter camera and image picking"
description: " "
date: 2023-09-29
tags: [collagemaker, camera, imagepicking]
comments: true
share: true
---

Creating a collage maker app can be a fun project to showcase your Flutter development skills. In this tutorial, we will explore how to integrate the camera functionality and image picking feature into a Flutter app.

## Setting Up the Project

To get started, let's create a new Flutter project. Open your command prompt or terminal and run the following command:

```
flutter create collage_maker_app
```

Once the project is created, navigate to the project directory using the `cd` command:

```
cd collage_maker_app
```

## Integrating Camera Functionality

Flutter provides a powerful plugin called `camera` to work with the device's camera. Let's add this plugin to our project by modifying the `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  camera: ^0.9.4+2
```

Save the file and run `flutter packages get` to download and install the plugin.

Next, let's add the necessary permissions for using the camera functionality by modifying the `AndroidManifest.xml` file located in `android/app/src/main`:

```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```

Now, create a new `CameraScreen.dart` file in the `lib` directory and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:camera/camera.dart';

class CameraScreen extends StatefulWidget {
  @override
  _CameraScreenState createState() => _CameraScreenState();
}

class _CameraScreenState extends State<CameraScreen> {
  CameraController cameraController;
  List<CameraDescription> cameras;

  @override
  void initState() {
    super.initState();
    _initializeCamera();
  }

  void _initializeCamera() async {
    cameras = await availableCameras();
    cameraController = CameraController(cameras[0], ResolutionPreset.medium);
    await cameraController.initialize();
    if (mounted) {
      setState(() {});
    }
  }

  @override
  void dispose() {
    cameraController?.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    if (cameraController == null || !cameraController.value.isInitialized) {
      return Container();
    }
    return Scaffold(
      appBar: AppBar(
        title: Text('Camera'),
      ),
      body: AspectRatio(
        aspectRatio: cameraController.value.aspectRatio,
        child: CameraPreview(cameraController),
      ),
    );
  }
}
```

We have created a `CameraScreen` widget that initializes the camera controller and displays the camera preview on the screen.

## Implementing Image Picking

To allow users to pick images from their device's gallery, we can use the `image_picker` plugin. Add the plugin to your project by modifying the `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  camera: ^0.9.4+2
  image_picker: ^0.7.4
```

Save the file and run `flutter packages get` to download and install the plugin.

Now, let's modify our existing `CameraScreen.dart` to include the image picking function. Add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:camera/camera.dart';
import 'package:image_picker/image_picker.dart';

class CameraScreen extends StatefulWidget {
  @override
  _CameraScreenState createState() => _CameraScreenState();
}

class _CameraScreenState extends State<CameraScreen> {
  CameraController cameraController;
  List<CameraDescription> cameras;
  final picker = ImagePicker();

  Future<void> _pickImage() async {
    final pickedFile = await picker.getImage(source: ImageSource.gallery);
    if (pickedFile != null) {
      // Do something with the picked image
    }
  }

  @override
  void initState() {
    super.initState();
    _initializeCamera();
  }

  void _initializeCamera() async {
    cameras = await availableCameras();
    cameraController = CameraController(cameras[0], ResolutionPreset.medium);
    await cameraController.initialize();
    if (mounted) {
      setState(() {});
    }
  }

  @override
  void dispose() {
    cameraController?.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    if (cameraController == null || !cameraController.value.isInitialized) {
      return Container();
    }
    return Scaffold(
      appBar: AppBar(
        title: Text('Camera'),
      ),
      body: AspectRatio(
        aspectRatio: cameraController.value.aspectRatio,
        child: CameraPreview(cameraController),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _pickImage,
        child: Icon(Icons.photo_library),
      ),
    );
  }
}
```

We have added a floating action button that triggers the image picking functionality when pressed. The picked image can be further processed or used to create collages.

## Conclusion

In this tutorial, we learned how to create a collage maker app using Flutter. We integrated the camera functionality using the `camera` plugin and allowed users to pick images from their device's gallery using the `image_picker` plugin. With these features in place, you can now explore adding collage creation and sharing capabilities to your app.

#flutter #collagemaker #camera #imagepicking
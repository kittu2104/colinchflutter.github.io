---
layout: post
title: "Building a panorama viewer and VR experience app with Flutter camera and image picking"
description: " "
date: 2023-09-29
tags: [appDevelopment]
comments: true
share: true
---

Flutter is a powerful framework that allows developers to build beautiful and interactive apps for multiple platforms using a single codebase. In this tutorial, we will explore how to build a panorama viewer and virtual reality (VR) experience app using Flutter's camera and image picking capabilities.

## Prerequisites
Before we start, make sure you have the following prerequisites installed on your machine:
- Flutter SDK
- Android Studio / Xcode (depending on your development environment)
- A compatible VR headset (such as Google Cardboard)

## Step 1: Setting up the Flutter project
1. Create a new Flutter project using the Flutter CLI command `flutter create panorama_viewer`.
2. Navigate to the project directory using `cd panorama_viewer`.
3. Open the project in your preferred IDE (Android Studio / VS Code).

## Step 2: Adding dependencies
Open the `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  camera: ^0.8.0
  permission_handler: ^14.0.0
  image_picker: ^0.8.3+1
```

Save the file and run `flutter pub get` command to fetch and install the added dependencies.

## Step 3: Requesting camera and storage permissions
To access the camera and image picker functionality, we need to request the necessary permissions from the user. Open the `main.dart` file and add the following code:

```dart
import 'package:permission_handler/permission_handler.dart';

void main() {
  WidgetsFlutterBinding.ensureInitialized();
  _requestPermissions().then((granted) {
    if (granted) {
      runApp(MyApp());
    } else {
      // Handle permission denial
    }
  });
}

Future<bool> _requestPermissions() async {
  var cameraPermission = await Permission.camera.request();
  var storagePermission = await Permission.storage.request();
  
  return cameraPermission.isGranted && storagePermission.isGranted;
}
```

This code ensures that the required permissions are requested when the app starts. If the permissions are granted, the `MyApp` widget is instantiated and the app is launched. Otherwise, you can handle the denial appropriately.

## Step 4: Implementing the panorama viewer and VR experience
1. Create a new Dart file named `panorama_viewer.dart` in the root directory.
2. Open the file and write the following code:

```dart
import 'package:flutter/material.dart';
import 'package:camera/camera.dart';
import 'package:image_picker/image_picker.dart';

class PanoramaViewer extends StatefulWidget {
  @override
  _PanoramaViewerState createState() => _PanoramaViewerState();
}

class _PanoramaViewerState extends State<PanoramaViewer> {
  List<CameraDescription>? cameras;
  CameraController? controller;
  bool _isCameraInitialized = false;
  XFile? _selectedImage;

  @override
  void initState() {
    super.initState();
    _initializeCamera();
  }

  Future<void> _initializeCamera() async {
    cameras = await availableCameras();
    controller = CameraController(cameras![0], ResolutionPreset.medium);
    await controller!.initialize();
    setState(() {
      _isCameraInitialized = true;
    });
  }

  Future<void> _pickImageFromGallery() async {
    final image = await ImagePicker().pickImage(source: ImageSource.gallery);
    setState(() {
      _selectedImage = image;
    });
  }

  @override
  void dispose() {
    controller?.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    if (!_isCameraInitialized) {
      return Container(); // Loading indicator could be shown here
    }

    return Scaffold(
      appBar: AppBar(
        title: const Text('Panorama Viewer'),
      ),
      body: _selectedImage != null
          ? Image.file(File(_selectedImage!.path))
          : Center(
              child: Text(
                'No image selected',
                style: TextStyle(fontSize: 20),
              ),
            ),
      floatingActionButton: FloatingActionButton(
        onPressed: _pickImageFromGallery,
        child: Icon(Icons.photo_library),
      ),
    );
  }
}
```

This code creates a Flutter widget called `PanoramaViewer` that displays either the selected image or a message if no image is selected. It also initializes the camera and allows the user to pick an image from the device's gallery.

## Step 5: Integrating the panorama viewer into the app
Replace the content of `lib/main.dart` with the following code:

```dart
import 'package:flutter/material.dart';

import 'panorama_viewer.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Panorama Viewer',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: PanoramaViewer(),
    );
  }
}
```

This code sets up the `PanoramaViewer` widget as the home screen of our app.

## Step 6: Testing the app
Connect your Android/iOS device to the computer and run the app using `flutter run`.

Once the app is launched on the device, you can select an image from the gallery by tapping the floating action button. The selected image will be displayed in the panorama viewer, providing an immersive VR experience when used with a compatible VR headset.

That's it! You've successfully built a panorama viewer and VR experience app using Flutter's camera and image picking capabilities. Explore further by adding more features and enhancing the user experience.

#flutter #VR #appDevelopment
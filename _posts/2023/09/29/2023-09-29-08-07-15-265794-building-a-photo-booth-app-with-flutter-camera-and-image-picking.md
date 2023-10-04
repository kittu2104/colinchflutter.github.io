---
layout: post
title: "Building a photo booth app with Flutter camera and image picking"
description: " "
date: 2023-09-29
tags: [photobooth]
comments: true
share: true
---

In this tutorial, we will walk through building a photo booth app using Flutter. We will leverage the Flutter camera package to capture images and the image_picker package to allow users to select images from their device's gallery. By combining these two packages, we can seamlessly create a full-fledged photo booth experience in our app.

## Prerequisites

Make sure you have the following set up before starting the implementation:

1. Flutter SDK installed on your machine.
2. A Flutter project set up.

## Installing the Required Packages

To get started, open your project and add the camera and image_picker packages to your `pubspec.yaml` file.

```yaml
dependencies:
  flutter:
    sdk: flutter
  camera: ^0.7.0
  image_picker: ^0.7.0
```

Run `flutter pub get` to download and install the packages.

## Implementing the Photo Booth App

### 1. Request Camera and Gallery Permissions

Add the following permissions to your `AndroidManifest.xml` file to request camera and gallery access in Android:

```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

For iOS, open `Info.plist` and add the following keys:

```xml
<key>NSCameraUsageDescription</key>
<string>Allow access to the camera to capture photos.</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>Allow access to the photo library to select photos.</string>
```

### 2. Create a Camera Widget

Create a new file `camera_widget.dart` and implement a `CameraWidget` that displays the live camera feed. We will use the `camera` package for this.

```dart
import 'package:flutter/material.dart';
import 'package:camera/camera.dart';

class CameraWidget extends StatelessWidget {
  final CameraController cameraController;

  const CameraWidget({Key key, this.cameraController}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    if (!cameraController.value.isInitialized) {
      return Container();
    }
    return AspectRatio(
      aspectRatio: cameraController.value.aspectRatio,
      child: CameraPreview(cameraController),
    );
  }
}
```

### 3. Use the Camera Widget in the Photo Booth Screen

In your main app file, import the necessary packages and create a `PhotoBoothScreen` where the camera and image picking functionality will be implemented.

```dart
import 'package:flutter/material.dart';
import 'package:camera/camera.dart';
import 'package:image_picker/image_picker.dart';
import 'camera_widget.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  final cameras = await availableCameras();
  final firstCamera = cameras.first;

  runApp(MyApp(
    firstCamera: firstCamera,
  ));
}

class MyApp extends StatelessWidget {
  final CameraDescription firstCamera;

  const MyApp({Key key, this.firstCamera}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Camera Demo',
      home: PhotoBoothScreen(firstCamera: firstCamera),
    );
  }
}

class PhotoBoothScreen extends StatefulWidget {
  final CameraDescription firstCamera;

  const PhotoBoothScreen({Key key, this.firstCamera}) : super(key: key);

  @override
  _PhotoBoothScreenState createState() => _PhotoBoothScreenState();
}

class _PhotoBoothScreenState extends State<PhotoBoothScreen> {
  CameraController _cameraController;
  ImagePicker _imagePicker = ImagePicker();

  @override
  void initState() {
    super.initState();
    _cameraController = CameraController(
      widget.firstCamera,
      ResolutionPreset.max,
    );
    _cameraController.initialize().then((_) {
      if (!mounted) return;
      setState(() {});
    });
  }

  @override
  void dispose() {
    _cameraController.dispose();
    super.dispose();
  }

  void _capturePhoto() async {
    final image = await _cameraController.takePicture();
    // Handle the captured image
  }

  void _pickFromGallery() async {
    final image = await _imagePicker.getImage(source: ImageSource.gallery);
    // Handle the picked image
  }

  @override
  Widget build(BuildContext context) {
    if (!_cameraController.value.isInitialized) {
      return Container();
    }
    return Scaffold(
      appBar: AppBar(
        title: Text('Photo Booth'),
      ),
      body: Stack(
        children: [
          CameraWidget(cameraController: _cameraController),
          Align(
            alignment: Alignment.bottomCenter,
            child: Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                IconButton(
                  icon: Icon(Icons.camera),
                  onPressed: _capturePhoto,
                ),
                IconButton(
                  icon: Icon(Icons.photo_library),
                  onPressed: _pickFromGallery,
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }
}
```

The `PhotoBoothScreen` widget utilizes the `CameraController` to capture photos and the `ImagePicker` to select images from the gallery. We display the live camera feed using the `CameraWidget` we created earlier.

### 4. Test the App

You can now run the app on an emulator or a physical device to test the photo booth functionality. Press the camera button to capture a photo and the gallery button to select an image from the device's gallery.

## Conclusion

Congratulations! You have successfully built a photo booth app using Flutter camera and image picking capabilities. You can enhance the app by adding filters, image editing options, and sharing functionality. Feel free to explore other features and possibilities to make your photo booth app even more interesting!

#flutter #photobooth
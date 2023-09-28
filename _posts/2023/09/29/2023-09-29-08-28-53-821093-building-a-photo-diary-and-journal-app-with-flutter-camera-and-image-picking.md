---
layout: post
title: "Building a photo diary and journal app with Flutter camera and image picking"
description: " "
date: 2023-09-29
tags: [flutter, flutterdevelopment]
comments: true
share: true
---

In today's digital age, capturing and preserving memories has become easier than ever. With the advancements in technology, we can now create personalized photo diaries and journals on our smartphones. In this blog post, we will explore how to build a photo diary and journal app using Flutter, a popular cross-platform framework, and its camera and image picking capabilities.

## Why Flutter?

Flutter is a powerful and flexible framework that allows developers to build high-quality, native mobile apps for both iOS and Android from a single codebase. It provides a rich set of widgets and tools that make it easy to create beautiful user interfaces and handle complex functionalities.

## Setting Up Flutter

To get started, make sure you have Flutter installed on your machine. You can follow the official Flutter installation guide to set it up: [flutter.dev/docs/get-started/install](https://flutter.dev/docs/get-started/install)

Once Flutter is set up, create a new Flutter project using the following command:

```
flutter create photo_diary_app
```

## Installing Dependencies

For our photo diary and journal app, we will be using the following dependencies:

1. `camera` - to access the device's camera and capture photos.
2. `image_picker` - to allow users to pick existing images from their device's gallery.

To install these dependencies, add them to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  camera: ^0.9.4+5
  image_picker: ^0.7.5+3
```

Then, run the following command in your terminal to fetch the dependencies:

```
flutter pub get
```

## Building the App

### 1. Adding Permissions

To use the camera and image picking functionalities, we need to add permissions in our `AndroidManifest.xml` (for Android) and `Info.plist` (for iOS) files. Open these files and add the following lines:

**Android (AndroidManifest.xml):**

```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera" />
```

**iOS (Info.plist):**

```xml
<key>NSCameraUsageDescription</key>
<string>Allow access to camera for capturing photos.</string>
<key>NSPhotoLibraryAddUsageDescription</key>
<string>Allow access to photo library for picking images.</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>Allow access to photo library for picking images.</string>
```

### 2. Implementing the Camera

To implement the camera functionality, we will create a new Dart file called `camera_screen.dart`. In this file, we will define a custom `CameraScreen` widget that displays the camera view. We will also use the `camera` package to control the camera and capture photos.

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
    // Obtain a list of available cameras on the device
    final cameras = await availableCameras();

    // Select the first camera from the list
    final firstCamera = cameras.first;

    // Initialize the camera controller
    _controller = CameraController(
      firstCamera,
      ResolutionPreset.medium,
    );

    // Initialize the controller future
    _initializeControllerFuture = _controller.initialize();
  }

  @override
  void dispose() {
    // Dispose the camera controller when not needed
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Camera'),
      ),
      body: FutureBuilder<void>(
        future: _initializeControllerFuture,
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.done) {
            // If the Future is complete, display the camera preview
            return CameraPreview(_controller);
          } else {
            // Otherwise, display a loading indicator
            return CircularProgressIndicator();
          }
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Take a photo when the FAB is pressed
          _takePhoto();
        },
        child: Icon(Icons.camera),
      ),
    );
  }
}
```

### 3. Adding Image Picking

Next, we will implement the image picking functionality using the `image_picker` package. We will create a new Dart file called `image_picker_screen.dart`. In this file, we will define a custom `ImagePickerScreen` widget that allows users to pick existing images from their device's gallery.

```dart
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';

class ImagePickerScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Image Picker'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            RaisedButton(
              onPressed: () {
                // Pick an image when the button is pressed
                _pickImage(context);
              },
              child: Text('Pick Image'),
            ),
          ],
        ),
      ),
    );
  }

  Future<void> _pickImage(BuildContext context) async {
    // Use the ImagePicker to pick an image from gallery
    final pickedImage = await ImagePicker().getImage(source: ImageSource.gallery);

    // Display the selected image
    if (pickedImage != null) {
      showDialog(
        context: context,
        builder: (context) => AlertDialog(
          title: Text('Selected Image'),
          content: Image.file(File(pickedImage.path)),
        ),
      );
    }
  }
}
```

### 4. Navigating Between Screens

To switch between the camera and image picking screens, we will use a `BottomNavigationBar` widget. Open the `main.dart` file and modify the `MyApp` widget as follows:

```dart
import 'package:flutter/material.dart';
import 'camera_screen.dart';
import 'image_picker_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Photo Diary App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MainScreen(),
    );
  }
}

class MainScreen extends StatefulWidget {
  @override
  _MainScreenState createState() => _MainScreenState();
}

class _MainScreenState extends State<MainScreen> {
  int _currentIndex = 0;
  List<Widget> _screens = [CameraScreen(), ImagePickerScreen()];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: _screens[_currentIndex],
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _currentIndex,
        onTap: (index) {
          setState(() {
            _currentIndex = index;
          });
        },
        items: [
          BottomNavigationBarItem(
            icon: Icon(Icons.camera),
            label: 'Camera',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.photo_library),
            label: 'Gallery',
          ),
        ],
      ),
    );
  }
}
```

## Conclusion

In this blog post, we explored how to build a photo diary and journal app using Flutter, the camera and image picking capabilities. We learned how to access the device's camera to capture photos and how to allow users to pick existing images from their gallery. By combining these functionalities, you can create a powerful app that helps users document their memories and create personalized photo diaries. With Flutter's extensive widget library and cross-platform support, the possibilities for building unique and creative apps are endless.

#flutter #flutterdevelopment
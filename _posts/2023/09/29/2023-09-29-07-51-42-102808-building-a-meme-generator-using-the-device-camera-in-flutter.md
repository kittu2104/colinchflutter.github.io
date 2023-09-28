---
layout: post
title: "Building a meme generator using the device camera in Flutter"
description: " "
date: 2023-09-29
tags: [flutter, memegenerator]
comments: true
share: true
---

With the rise of memes, it's no surprise that many developers have started building meme-related applications. In this tutorial, we will guide you through building a meme generator app using the device camera in Flutter. Let's get started!

## Prerequisites
Before we begin, make sure you have the following installed:
- Flutter SDK
- Android Studio or any other IDE of your choice
- A device or emulator to run the app

## Step 1: Set up the Flutter project
 1. Open your terminal or command prompt and create a new Flutter project by running:
```sh
flutter create meme_generator_app
```

 2. Open the project in your preferred IDE.

## Step 2: Set up dependencies
To use the device camera in the app, we need to add the `camera` and `image_picker` packages to our `pubspec.yaml` file. Open the file and add the following lines under `dependencies`:
```yaml
dependencies:
  flutter:
    sdk: flutter
  camera: any
  image_picker: any
```
Save the file and run `flutter pub get` to fetch the new packages.

## Step 3: Request camera permission
In order to access the device camera, we need to add the necessary permissions to the `AndroidManifest.xml` file. Locate the file under the `android/app/src/main` directory and add the following lines within the `<manifest>` tag:
```xml
<!-- Required to access the device camera -->
<uses-permission android:name="android.permission.CAMERA"/>
```
Save the file.

## Step 4: Implement the meme generator
In the `lib` directory, open the `main.dart` file and update the code as follows:

```dart
import 'dart:io';

import 'package:flutter/material.dart';
import 'package:camera/camera.dart';
import 'package:image_picker/image_picker.dart';

List<CameraDescription> cameras;

Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  cameras = await availableCameras();
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Meme Generator',
      home: MemeGenerator(),
    );
  }
}

class MemeGenerator extends StatefulWidget {
  @override
  _MemeGeneratorState createState() => _MemeGeneratorState();
}

class _MemeGeneratorState extends State<MemeGenerator> {
  File capturedImage;

  Future<void> _captureImageFromCamera() async {
    final picker = ImagePicker();
    final image = await picker.getImage(source: ImageSource.camera);
    setState(() {
      capturedImage = File(image.path);
    });
  }

  Future<void> _pickImageFromGallery() async {
    final picker = ImagePicker();
    final image = await picker.getImage(source: ImageSource.gallery);
    setState(() {
      capturedImage = File(image.path);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Meme Generator')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            capturedImage != null
                ? Image.file(capturedImage)
                : Text('No image selected'),
            SizedBox(height: 20),
            RaisedButton(
              child: Text('Take Photo'),
              onPressed: _captureImageFromCamera,
            ),
            RaisedButton(
              child: Text('Pick from Gallery'),
              onPressed: _pickImageFromGallery,
            ),
          ],
        ),
      ),
    );
  }
}
```

The code sets up the basic structure of the app, including the camera and image picker functionalities. The `MemeGenerator` widget displays the selected image or the text "No image selected" if no image is chosen.

## Step 5: Build and run the app
Now that we have implemented the meme generator, let's build and run the app. Open your terminal or command prompt in the project directory and run:
```sh
flutter run
```

## Conclusion
In this tutorial, we created a meme generator app using the device camera in Flutter. We covered setting up the Flutter project, adding necessary dependencies, requesting camera permission, and implementing the meme generator functionality. Feel free to enhance the app by adding text overlay features, image manipulation options, or even integrating meme templates. Get creative and have fun building your own meme generator app! #flutter #memegenerator
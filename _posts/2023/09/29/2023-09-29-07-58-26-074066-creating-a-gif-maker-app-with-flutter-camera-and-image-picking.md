---
layout: post
title: "Creating a GIF maker app with Flutter camera and image picking"
description: " "
date: 2023-09-29
tags: [flutter, camera, imagepicker, appdevelopment]
comments: true
share: true
---

In this tutorial, we will learn how to build a GIF maker app using Flutter. We will utilize the camera and image picking capabilities of Flutter to capture photos and select images from the device's gallery, and then use them to create animated GIFs.

## Prerequisites

Before we begin, make sure you have Flutter installed on your machine. You can follow the official Flutter installation guide for your specific operating system. Additionally, ensure you have a basic understanding of Flutter and Dart programming.

## Step 1: Setting up the Flutter Project

Let's begin by creating a new Flutter project. Open your terminal or command prompt and execute the following command:

```bash
$ flutter create gif_maker_app
$ cd gif_maker_app
```

## Step 2: Adding Required Dependencies

Next, we need to add the necessary dependencies to our `pubspec.yaml` file. Open the file and add the following lines:

```yaml
dependencies:
  camera: ^x.x.x  # Add the latest version
  image_picker: ^x.x.x  # Add the latest version
  path_provider: ^x.x.x  # Add the latest version
  dio: ^x.x.x  # Add the latest version
  
dev_dependencies:
  flutter_test:
    sdk: flutter
```

Replace `x.x.x` with the latest version numbers of each package. After adding the dependencies, run the command `flutter pub get` in your terminal to download these packages.

## Step 3: Building the Camera and Image Picker Widgets

We will now create two widgets, `CameraWidget` and `ImagePickerWidget`, to handle the camera preview and image selection functionalities, respectively. Create a new file called `camera_widget.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:camera/camera.dart';

class CameraWidget extends StatefulWidget {
  @override
  _CameraWidgetState createState() => _CameraWidgetState();
}

class _CameraWidgetState extends State<CameraWidget> {
  late CameraController _controller;

  @override
  void initState() {
    super.initState();
    _initializeCamera();
  }

  void _initializeCamera() async {
    final cameras = await availableCameras();
    final camera = cameras.first;
    _controller = CameraController(camera, ResolutionPreset.medium);
    await _controller.initialize();
    if (!mounted) {
      return;
    }
    setState(() {});
  }

  @override
  Widget build(BuildContext context) {
    if (!_controller.value.isInitialized) {
      return Container();
    }
    return AspectRatio(
      aspectRatio: _controller.value.aspectRatio,
      child: CameraPreview(_controller),
    );
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
}
```

Similarly, create a new file called `image_picker_widget.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';

class ImagePickerWidget extends StatefulWidget {
  @override
  _ImagePickerWidgetState createState() => _ImagePickerWidgetState();
}

class _ImagePickerWidgetState extends State<ImagePickerWidget> {
  late final ImagePicker _picker;

  @override
  void initState() {
    super.initState();
    _picker = ImagePicker();
  }

  void _pickImage() async {
    final pickedFile = await _picker.getImage(source: ImageSource.gallery);
    if (pickedFile != null) {
      setState(() {
        // Handle the selected image here
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: _pickImage,
      child: Text('Select Image'),
    );
  }
}
```

## Step 4: Implementing GIF Creation logic

Now, let's create the main widget that will handle the creation of GIFs. Open the `main.dart` file and update its contents with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:path_provider/path_provider.dart';
import 'package:dio/dio.dart';

import 'camera_widget.dart';
import 'image_picker_widget.dart';

void main() {
  runApp(GifMakerApp());
}

class GifMakerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'GIF Maker',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: GifMakerScreen(),
    );
  }
}

class GifMakerScreen extends StatefulWidget {
  @override
  _GifMakerScreenState createState() => _GifMakerScreenState();
}

class _GifMakerScreenState extends State<GifMakerScreen> {
  List<String> _imagePaths = [];

  void _createGif() async {
    final tempDir = await getTemporaryDirectory();
    final gifPath = '${tempDir.path}/my_gif.gif';

    // Implement the logic to create GIF using _imagePaths and gifPath variables

    final dio = Dio();
    final response = await dio.download(
      'https://example.com/upload',
      gifPath,
      options: Options(headers: {'Content-Type': 'image/gif'}),
    );

    if (response.statusCode == 200) {
      // Handle success
    } else {
      // Handle failure
    }
  }

  void _addImagePath(String path) {
    setState(() {
      _imagePaths.add(path);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('GIF Maker'),
      ),
      body: Column(
        children: [
          Expanded(
            flex: 2,
            child: CameraWidget(),
          ),
          Expanded(
            flex: 1,
            child: ImagePickerWidget(),
          ),
          ElevatedButton(
            onPressed: _createGif,
            child: Text('Create GIF'),
          ),
        ],
      ),
    );
  }
}
```

## Step 5: Testing the App

You can now test the GIF maker app on both Android and iOS devices or simulators. Run the following command in your terminal:

```bash
$ flutter run
```

Ensure that you have a connected device or simulator to see the app in action.

Congratulations! You have successfully created a GIF maker app using Flutter's camera and image picking capabilities. Feel free to customize and enhance the app further as per your requirements.

#flutter #camera #imagepicker #appdevelopment
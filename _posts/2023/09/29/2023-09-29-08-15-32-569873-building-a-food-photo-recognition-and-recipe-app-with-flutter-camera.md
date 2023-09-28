---
layout: post
title: "Building a food photo recognition and recipe app with Flutter camera"
description: " "
date: 2023-09-29
tags: [flutter, foodrecognition]
comments: true
share: true
---

In today's digital age, food photography has become a popular trend. Imagine being able to take a photo of a dish and instantly getting information about it, along with a recipe to recreate it. With the help of Flutter and its camera plugin, we can build a food photo recognition and recipe app that brings this idea to life.

## The Power of Flutter Camera Plugin

Flutter provides a robust camera plugin, which allows us to easily integrate camera functionality into our app. Let's start by adding the camera plugin to our Flutter project by editing the `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter

  camera: ^0.9.4+5
```

After saving the `pubspec.yaml` file, run `flutter packages get` in the terminal to fetch the camera plugin.

## Capturing and Analyzing Food Photos

To capture food photos, we can make use of the Flutter camera plugin's features. Here's a simple example of how we can capture a photo:

```dart
import 'package:camera/camera.dart';
import 'package:flutter/material.dart';

class CameraScreen extends StatefulWidget {
  final List<CameraDescription> cameras;

  CameraScreen({required this.cameras});

  @override
  _CameraScreenState createState() => _CameraScreenState();
}

class _CameraScreenState extends State<CameraScreen> {
  late CameraController _controller;
  late Future<void> _initializeControllerFuture;

  @override
  void initState() {
    super.initState();
    _controller = CameraController(
      widget.cameras[0],
      ResolutionPreset.medium,
    );
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
        title: Text('Foodify Camera'),
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
          _takePhoto(context);
        },
      ),
    );
  }

  void _takePhoto(BuildContext context) async {
    try {
      await _initializeControllerFuture;
      final image = await _controller.takePicture();
      Navigator.push(
        context,
        MaterialPageRoute(
          builder: (context) => PhotoPreviewScreen(
            imagePath: image?.path ?? '',
          ),
        ),
      );
    } catch (e) {
      print(e);
    }
  }
}
```

In the above code, we create a `CameraScreen` widget that initializes a `CameraController` and displays the camera preview. When the user taps on the camera button, we capture the photo and navigate to the `PhotoPreviewScreen`.

## Food Image Recognition with AI

To recognize the food within the captured photo, we can use a pre-trained machine learning model. One popular option is the TensorFlow Lite model, which you can train with food images.

Once you have the TensorFlow Lite model ready, you can integrate it into your Flutter app by using the `tflite_flutter` package. This package allows you to execute TensorFlow Lite models on mobile devices.

Here's an example code snippet to perform image recognition using a TensorFlow Lite model:

```dart
import 'dart:io';
import 'package:flutter/material.dart';
import 'package:tflite_flutter/tflite_flutter.dart';

class PhotoPreviewScreen extends StatefulWidget {
  final String imagePath;

  PhotoPreviewScreen({required this.imagePath});

  @override
  _PhotoPreviewScreenState createState() => _PhotoPreviewScreenState();
}

class _PhotoPreviewScreenState extends State<PhotoPreviewScreen> {
  bool _isLoading = false;
  Interpreter? _interpreter;
  List<String> _foodLabels = [];

  @override
  void initState() {
    super.initState();
    _loadModel();
  }

  @override
  void dispose() {
    _interpreter?.close();
    super.dispose();
  }

  void _loadModel() async {
    setState(() {
      _isLoading = true;
    });

    try {
      final modelFile = await File('assets/food_recognition_model.tflite').readAsBytes();
      final labelFile = await File('assets/food_labels.txt').readAsString();

      _interpreter = await Interpreter.fromBuffer(modelFile);

      setState(() {
        _foodLabels = labelFile.split('\n');
        _isLoading = false;
      });
    } catch (e) {
      print(e);
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Foodify Photo Preview'),
      ),
      body: _isLoading
          ? Center(child: CircularProgressIndicator())
          : Column(
              children: [
                Image.file(File(widget.imagePath)),
                ElevatedButton(
                  onPressed: _classifyFood,
                  child: Text('Recognize Food'),
                ),
                _foodLabels.isNotEmpty
                    ? Text(_foodLabels[0])
                    : SizedBox(),
              ],
            ),
    );
  }

  Future<void> _classifyFood() async {
    final image = File(widget.imagePath);
    if (!_isLoading && _interpreter != null && image.existsSync()) {
      var inputImage = _preprocessImage(image);
      var outputResults = List.filled(1, [0.0]);

      _interpreter!.run(inputImage.buffer, outputResults.buffer);

      var predictedFoodIndex = outputResults[0].indexOf(outputResults[0].reduce((a, b) => a > b ? a : b));
      var predictedFood = _foodLabels[predictedFoodIndex];

      setState(() {
        _foodLabels.clear();
        _foodLabels.add(predictedFood);
      });
    }
  }

  Float32List _preprocessImage(File image) {
    // Perform image preprocessing before passing it to the model
    // e.g., resizing, normalization, etc.
    // ...

    return Float32List.fromList([]);
  }
}
```

In the above code, we create a `PhotoPreviewScreen` widget that loads the TensorFlow Lite model and performs food image recognition. We display the captured photo and provide a button to recognize the food in the image. The recognized food name is displayed below the button.

## Conclusion

By combining the power of Flutter and the camera plugin with TensorFlow Lite for image recognition, we can build a food photo recognition and recipe app. Users can capture food photos, have them recognized, and get recipe suggestions based on the recognized dish. With a few more features, such as storing favorite recipes and sharing on social media, you'll have a complete and engaging app for all food enthusiasts. Start building and explore the endless possibilities of food and technology!

#flutter #foodrecognition
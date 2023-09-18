---
layout: post
title: "Implementing face recognition and detection with Flutter's facial recognition widget"
description: " "
date: 2023-09-14
tags: [FacialRecognition]
comments: true
share: true
---

In this tutorial, we will explore how to implement face recognition and detection using Flutter's facial recognition widget. Face recognition and detection have become popular features in many applications, from personalized filters in social media apps to presence detection in smart homes. With the facial recognition widget provided by the Flutter framework, we can easily incorporate these features into our Flutter applications.

## Installing the required packages
To get started, we need to install the necessary packages for face recognition and detection in Flutter. Let's add the `firebase_ml_vision` package to our `pubspec.yaml` file:

```
dependencies:
  flutter:
    sdk: flutter
    
  firebase_ml_vision: ^0.9.9
```
After adding the package to the dependencies, run `flutter pub get` to download and link the package.

## Setting up the UI
First, let's set up a basic UI to display the camera preview and the detected faces. In your Flutter project, open the `main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:firebase_ml_vision/firebase_ml_vision.dart';
import 'dart:ui' as ui;

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Face Recognition',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: FaceRecognitionScreen(),
    );
  }
}

class FaceRecognitionScreen extends StatefulWidget {
  @override
  _FaceRecognitionScreenState createState() => _FaceRecognitionScreenState();
}

class _FaceRecognitionScreenState extends State<FaceRecognitionScreen> {
  CameraImage _currentImage;
  List<Face> _detectedFaces = [];

  void _processImage(CameraImage image) async {
    final FirebaseVisionImage visionImage = FirebaseVisionImage.fromBytes(
      image.planes[0].bytes,
      FirebaseVisionImageMetadata(
        rawFormat: image.format.raw,
        size: Size(image.width.toDouble(), image.height.toDouble()),
        rotation: ImageRotation.rotation90,
        planeData: image.planes.map((Plane plane) {
          return FirebaseVisionImagePlaneMetadata(
            bytesPerRow: plane.bytesPerRow,
            height: plane.height,
            width: plane.width,
          );
        }).toList(),
      ),
    );

    final FaceDetector faceDetector = FirebaseVision.instance.faceDetector(
      FaceDetectorOptions(
        mode: FaceDetectorMode.fast,
        enableLandmarks: true,
      ),
    );

    final List<Face> faces = await faceDetector.processImage(visionImage);
    setState(() {
      _currentImage = image;
      _detectedFaces = faces;
    });

    faceDetector.close();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Face Recognition'),
      ),
      body: Column(
        children: <Widget>[
          Expanded(
            child: Container(
              child: _currentImage != null
                  ? CustomPaint(
                      foregroundPainter: FacePainter(_currentImage, _detectedFaces),
                      child: AspectRatio(
                        aspectRatio: _currentImage.width.toDouble() /
                            _currentImage.height.toDouble(),
                        child: CameraPreview(_currentImage),
                      ),
                    )
                  : Container(),
            ),
          ),
        ],
      ),
    );
  }
}

class FacePainter extends CustomPainter {
  final CameraImage _image;
  final List<Face> _faces;

  FacePainter(this._image, this._faces);

  @override
  void paint(Canvas canvas, Size size) {
    final Paint paint = Paint()
      ..style = PaintingStyle.stroke
      ..strokeWidth = 2.0
      ..color = Colors.red;

    for (Face face in _faces) {
      final Rect boundingBox = Rect.fromLTRB(
        face.boundingBox.left,
        face.boundingBox.top,
        face.boundingBox.right,
        face.boundingBox.bottom,
      );

      canvas.drawRect(
        boundingBox,
        paint,
      );
    }
  }

  @override
  bool shouldRepaint(FacePainter oldDelegate) {
    return _image != oldDelegate._image || _faces != oldDelegate._faces;
  }
}
```

## Running the App
Now that we have implemented the face recognition and detection functionality, let's run the app on a device or emulator. Run the following command in the terminal to start the Flutter application:

```
flutter run
```

Make sure your device or emulator has a camera. Once the app is running, you will see a camera preview with the detected faces highlighted in red rectangles.

## Conclusion
In this tutorial, we learned how to implement face recognition and detection with Flutter's facial recognition widget. We utilized the `firebase_ml_vision` package to process the camera image and detect faces. Using the provided code, you can further extend the functionality by adding features like face recognition and tracking. Happy coding!

\#Flutter #FacialRecognition
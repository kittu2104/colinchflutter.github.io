---
layout: post
title: "Implementing image recognition and OCR with GetX"
description: " "
date: 2023-09-29
tags: [flutter, GetX, imageRecognition]
comments: true
share: true
---

In this blog post, we will explore how to implement image recognition and optical character recognition (OCR) in a Flutter application using the GetX package. GetX is a powerful state management library that simplifies and accelerates the development process.

## What is Image Recognition?

Image recognition is the process of identifying and detecting objects or patterns in digital images or photographs. With the advancement of machine learning and deep learning algorithms, image recognition has become more accurate and reliable in recent years. In this tutorial, we will use the GetX package to implement image recognition in Flutter.

## What is OCR?

Optical Character Recognition (OCR) is a technology that extracts text from images or scanned documents. It allows us to convert text in images into machine-readable format, making it possible to perform text analysis, translation, and other operations. In this tutorial, we will leverage the power of GetX to implement OCR functionality in our Flutter app.

## Getting Started

To get started, make sure you have Flutter and the GetX package installed in your development environment. If you haven't installed Flutter yet, you can follow the official Flutter installation guide. To install the GetX package, add the following dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  get: ^4.1.4
```

After adding the dependency, run the command `flutter pub get` in your terminal to download and install the package.

## Implementing Image Recognition

To implement image recognition with GetX, we need to use a pre-trained model for object detection. There are various pre-trained models available, such as MobileNet and YOLO (You Only Look Once), that can be used for image recognition tasks. We can use the `tflite` package to load and run the pre-trained model in Flutter.

First, download the pre-trained model that you want to use for image recognition. Once you have the model file, add it to your project's assets folder and update the `pubspec.yaml` file to include the model file:

```yaml
flutter:
  assets:
    - assets/model.tflite
```

Next, create a new file called `image_recognition_controller.dart` and implement the following code:

```dart
import 'package:get/get.dart';
import 'package:tflite/tflite.dart';

class ImageRecognitionController extends GetxController {
  Future<void> loadImageRecognitionModel() async {
    await Tflite.loadModel(
      model: "assets/model.tflite",
      labels: "assets/labels.txt",
    );
  }

  Future<List<dynamic>> recognizeImage(String imagePath) async {
    final result = await Tflite.runModelOnImage(
      path: imagePath,
    );
    return result;
  }
}
```

In the code above, we define a `ImageRecognitionController` class that extends the `GetXController` class provided by GetX. In the `loadImageRecognitionModel` method, we load the pre-trained model using the `Tflite.loadModel` method. We specify the model file path and the path to the labels file, which contains the names of the objects that the model can recognize.

The `recognizeImage` method takes an image path as input and runs the image recognition model on the specified image. The method returns a list of detected objects along with their probabilities.

To use the `ImageRecognitionController` in our Flutter app, we can create a GetX controller instance in our view and call the necessary methods:

```dart
class MyHomePage extends StatelessWidget {
  final ImageRecognitionController _controller = Get.put(ImageRecognitionController());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Image Recognition'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: () async {
                await _controller.loadImageRecognitionModel();
              },
              child: Text('Load Model'),
            ),
            ElevatedButton(
              onPressed: () async {
                final result = await _controller.recognizeImage('assets/image.jpg');
                print(result);
              },
              child: Text('Recognize Image'),
            ),
          ],
        ),
      ),
    );
  }
}
```

In the code above, we create an instance of the `ImageRecognitionController` using `Get.put` and call the `loadImageRecognitionModel` method when the "Load Model" button is pressed. When the "Recognize Image" button is pressed, we call the `recognizeImage` method and print the result to the console.

## Implementing OCR

To implement OCR with GetX, we will use the `firebase_ml_vision` plugin, which provides OCR functionality in Flutter. The plugin integrates with Firebase ML Kit, a powerful library for machine learning on mobile devices.

First, add the `firebase_ml_vision` plugin to your `pubspec.yaml` file:

```yaml
dependencies:
  firebase_ml_vision: ^0.11.0+1
```

After adding the dependency, run `flutter pub get` to install the package.

Next, create a new file called `ocr_controller.dart` and implement the following code:

```dart
import 'package:get/get.dart';
import 'package:firebase_ml_vision/firebase_ml_vision.dart';

class OCRController extends GetxController {
  Future<List<VisionText>> recognizeText(String imagePath) async {
    final image = FirebaseVisionImage.fromFilePath(imagePath);
    final textRecognizer = FirebaseVision.instance.textRecognizer();
    final result = await textRecognizer.processImage(image);
    return result.text;
  }
}
```

In the code above, we define a `OCRController` class that extends the `GetXController` class provided by GetX. The `recognizeText` method takes an image path as input, creates a `FirebaseVisionImage` object from the image path, and uses the `textRecognizer` to process the image and extract the text.

To use the `OCRController` in our Flutter app, we can create a GetX controller instance in our view and call the necessary methods:

```dart
class MyHomePage extends StatelessWidget {
  final OCRController _controller = Get.put(OCRController());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('OCR'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: () async {
                final result = await _controller.recognizeText('assets/image.jpg');
                print(result);
              },
              child: Text('Recognize Text'),
            ),
          ],
        ),
      ),
    );
  }
}
```

In the code above, we create an instance of the `OCRController` using `Get.put` and call the `recognizeText` method when the "Recognize Text" button is pressed. We print the result, which is a list of `VisionText` objects representing the recognized text, to the console.

## Conclusion

In this tutorial, we have seen how to implement image recognition and OCR in a Flutter application using the GetX package. We leveraged the power of pre-trained models with the `tflite` package for image recognition and integrated the `firebase_ml_vision` plugin for OCR functionality. With GetX, we were able to simplify the state management and easily use these powerful features in our Flutter app.

#flutter #GetX #imageRecognition #OCR
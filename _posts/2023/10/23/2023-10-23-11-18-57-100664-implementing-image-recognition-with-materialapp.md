---
layout: post
title: "Implementing image recognition with MaterialApp."
description: " "
date: 2023-10-23
tags: [image]
comments: true
share: true
---

Image recognition is a fascinating technology that allows computers to identify and classify objects in images or videos. With the help of machine learning models and neural networks, it becomes possible to develop applications that can recognize and interpret visual data.

In this tutorial, we will explore how to implement image recognition using the `MaterialApp` widget in Flutter. Flutter is a powerful cross-platform framework for building native-like applications, and the `MaterialApp` widget is a fundamental component for creating visually appealing and responsive UIs.

## Table of Contents
- [Setting up the Project](#setting-up-the-project)
- [Integrating Image Recognition](#integrating-image-recognition)
- [Displaying Recognition Results](#displaying-recognition-results)
- [Conclusion](#conclusion)

## Setting up the Project

To get started, you need to have Flutter installed on your system. If you haven't installed Flutter yet, please refer to the official Flutter documentation for instructions on how to set it up.

Once you have Flutter installed, create a new Flutter project using the following command:

```bash
$ flutter create image_recognition_app
```

Now, navigate to the project directory:

```bash
$ cd image_recognition_app
```

Open the project in your favorite code editor. We'll be working with `main.dart`, which is the entry point for our application.

## Integrating Image Recognition

To implement image recognition, we need to use a pre-trained machine learning model. There are various models available, such as TensorFlow Lite and Core ML. For this tutorial, we will be using TensorFlow Lite.

First, add the TensorFlow Lite Flutter plugin to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  tflite: ^1.2.0
```

Run `flutter pub get` to get the dependencies.

Next, download a pre-trained TensorFlow Lite model for image recognition, or use the example model provided by TensorFlow. Place the model inside a `assets` folder in your project directory.

For simplicity, we'll use the example TensorFlow Lite model. You can download it from the TensorFlow GitHub repository: [TensorFlow Lite Example Model](https://github.com/tensorflow/examples/raw/master/lite/examples/image_classification/android/app/src/main/assets/mobilenet_v1_1.0_224.tflite)

After downloading the model, update your `pubspec.yaml` file to include the model file as an asset:

```yaml
flutter:
  assets:
    - assets/mobilenet_v1_1.0_224.tflite
```

Now, let's write the code to load the TensorFlow Lite model and make predictions:

```dart
import 'dart:io';

import 'package:flutter/material.dart';
import 'package:tflite/tflite.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  bool _loading = true;
  List<dynamic> _recognitions;

  @override
  void initState() {
    super.initState();
    loadModel();
  }

  Future<void> loadModel() async {
    await Tflite.loadModel(
      model: 'assets/mobilenet_v1_1.0_224.tflite',
      labels: 'assets/labels.txt',
    );
    setState(() {
      _loading = false;
    });
  }

  @override
  void dispose() {
    Tflite.close();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Image Recognition'),
        ),
        body: Center(
          child: _loading
              ? CircularProgressIndicator()
              : Text('Model loaded and ready for predictions!'),
        ),
      ),
    );
  }
}
```

This code sets up the basic structure for our application. The `loadModel` function loads the model and associated labels, while the `build` method displays a loading indicator while the model is being loaded.

## Displaying Recognition Results

To display the results of our image recognition, we can modify the UI to show the top predictions made by the TensorFlow Lite model. Add the following code inside the `build` method:

```dart
...
body: Center(
  child: _loading
      ? CircularProgressIndicator()
      : Column(
          children: [
            Image.asset('assets/image.jpg'), // Replace with your image
            SizedBox(height: 16),
            Text(
              'Predictions:',
              style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 8),
            _recognitions != null
                ? Column(
                    children: _recognitions.map((res) {
                      return Text(
                        '${res['label']}: ${res['confidence'].toStringAsFixed(2)}',
                        style: TextStyle(fontSize: 16),
                      );
                    }).toList(),
                  )
                : Container(),
          ],
        ),
),
...
```

This code displays the loaded image, followed by the recognition results. The predictions are shown as a list of labels and confidence scores.

Finally, update the code inside the `loadModel` method to include recognition predictions:

```dart
Future<void> loadModel() async {
  await Tflite.loadModel(
    model: 'assets/mobilenet_v1_1.0_224.tflite',
    labels: 'assets/labels.txt',
  );
  setState(() {
    _loading = false;
  });

  classifyImage();
}

Future<void> classifyImage() async {
  setState(() {
    _loading = true;
  });

  var recognitions = await Tflite.runModelOnImage(
    path: 'assets/image.jpg', // Replace with your image
    numResults: 5,
    threshold: 0.5,
    imageMean: 127.5,
    imageStd: 127.5,
  );

  setState(() {
    _loading = false;
    _recognitions = recognitions;
  });
}
```

Here, we've added the `classifyImage` method that runs the image recognition model on the provided image. It processes the image and returns a list of recognition results. We update the UI with the results by setting the `_recognitions` variable.

## Conclusion

Congratulations! You've successfully implemented image recognition using the `MaterialApp` widget in Flutter. You've learned how to integrate a TensorFlow Lite model for image recognition and display the recognition results in the UI.

Feel free to experiment further by trying different TensorFlow Lite models or building more complex applications around image recognition. Flutter provides a rich set of tools and widgets to help you create powerful and visually stunning applications. Happy coding!

**References:**
- Flutter Official Documentation: [https://flutter.dev](https://flutter.dev)
- TensorFlow Lite Flutter Plugin: [https://pub.dev/packages/tflite](https://pub.dev/packages/tflite)
- TensorFlow Lite Example Model: [https://github.com/tensorflow/examples/raw/master/lite/examples/image_classification/android/app/src/main/assets/mobilenet_v1_1.0_224.tflite](https://github.com/tensorflow/examples/raw/master/lite/examples/image_classification/android/app/src/main/assets/mobilenet_v1_1.0_224.tflite) 

#flutter #image-recognition
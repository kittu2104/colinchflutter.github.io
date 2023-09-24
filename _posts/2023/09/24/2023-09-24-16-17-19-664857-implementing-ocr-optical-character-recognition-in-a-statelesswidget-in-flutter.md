---
layout: post
title: "Implementing OCR (Optical Character Recognition) in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [Flutter]
comments: true
share: true
---

![OCR](ocr-image.jpg) *#OCR #Flutter*

Optical Character Recognition (OCR) is a technology that enables you to extract text from images or scanned documents and convert it into machine-readable text. In this blog post, we will explore how to implement OCR in a StatelessWidget using the Flutter framework.

## Setting up the project

Before we dive into the implementation, make sure you have Flutter SDK installed on your machine. You can download and install Flutter from the official website: https://flutter.dev/

Once you have Flutter installed, create a new Flutter project using the following command:

```shell
flutter create ocr_flutter
```

After the project is created, navigate to the project directory:

```shell
cd ocr_flutter
```

## Dependencies

To add OCR functionality to our Flutter app, we'll use the `flutter_ocr` package. This package provides easy integration with OCR APIs. Update the `pubspec.yaml` file with the following dependency:

```yaml
dependencies:
  flutter_ocr: ^1.0.0
```

Save the file and run the following command to fetch the dependencies:

```shell
flutter pub get
```

## Implementing the OCR logic

In our Flutter project, let's create a new file called `ocr_screen.dart` under the `lib` directory. This file will contain our StatelessWidget code.

Inside the `ocr_screen.dart` file, add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_ocr/flutter_ocr.dart';

class OcrScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('OCR Example'),
      ),
      body: Center(
        child: RaisedButton(
          child: Text('Extract Text'),
          onPressed: () async {
            String imagePath = 'path_to_your_image.jpg';
            String text = await FlutterOcr.extractText(imagePath);
            print(text);
          },
        ),
      ),
    );
  }
}
```

In the above code, we import the necessary packages, create a StatelessWidget called `OcrScreen`, and define the UI with a `RaisedButton` that triggers the OCR extraction logic when pressed.

Make sure to replace `'path_to_your_image.jpg'` with the path to your actual image file. 

## Adding the OcrScreen to the app

Now, open the `main.dart` file under the `lib` directory. Remove the default code and add the following:

```dart
import 'package:flutter/material.dart';
import 'ocr_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'OCR Flutter',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: OcrScreen(),
    );
  }
}
```

In the above code, we define the `MyApp` StatelessWidget that sets up the Flutter app with a title and a theme. We set `OcrScreen()` as the home screen of the app.

## Running the app

Now, we can run our Flutter app and test the OCR functionality.

Connect your device or emulator and run the following command:

```shell
flutter run
```

The app should launch on your device or emulator. When you click the "Extract Text" button, the OCR logic will extract text from the provided image path and print it on the console.

Congratulations! You have successfully implemented OCR in a StatelessWidget in Flutter.

I hope you found this tutorial helpful. Feel free to explore the `flutter_ocr` package further to enhance your OCR implementation.

Happy coding! 🚀
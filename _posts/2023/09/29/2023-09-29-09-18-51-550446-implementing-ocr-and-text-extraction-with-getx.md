---
layout: post
title: "Implementing OCR and text extraction with GetX"
description: " "
date: 2023-09-29
tags: [Flutter, GetX, TextExtraction]
comments: true
share: true
---

In this tutorial, we will explore how to implement Optical Character Recognition (OCR) and text extraction in a Flutter application using the GetX package. OCR allows us to extract text from images or documents, which can be useful in various scenarios such as digitizing printed documents, extracting information from business cards, or even building a mobile scanner app.

## Prerequisites

To follow along with this tutorial, you will need:

- Flutter SDK installed on your machine
- An IDE of your choice (such as Visual Studio Code or Android Studio)
- GetX package added as a dependency in your Flutter project

## Getting Started

Let's start by adding the GetX package as a dependency in our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  get: ^4.1.4
```

Then, run the command `flutter pub get` to fetch and add the package to your project.

## Using the `image_picker` Package

To enable image selection from the device's gallery or camera, we will use the `image_picker` package. Add it as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  image_picker: ^0.8.4
```

Again, run `flutter pub get` to fetch and add the package to your project.

## Creating the OCR Service

Next, let's create a dedicated service class for our OCR functionality. Inside the `services` directory, create a new file called `ocr_service.dart` with the following code:

```dart
import 'dart:io';

import 'package:image_picker/image_picker.dart';
import 'package:firebase_ml_vision/firebase_ml_vision.dart';

class OCRService {
  final ImagePicker _imagePicker = ImagePicker();

  Future<String?> extractTextFromImage() async {
    final XFile? imageFile =
        await _imagePicker.pickImage(source: ImageSource.gallery);

    if (imageFile != null) {
      final File image = File(imageFile.path);
      final FirebaseVisionImage visionImage =
          FirebaseVisionImage.fromFile(image);
      final TextRecognizer textRecognizer =
          FirebaseVision.instance.textRecognizer();

      final VisionText visionText =
          await textRecognizer.processImage(visionImage);

      String extractedText = '';
      for (TextBlock block in visionText.blocks) {
        for (TextLine line in block.lines) {
          for (TextElement element in line.elements) {
            extractedText += '${element.text} ';
          }
        }
      }

      textRecognizer.close();

      return extractedText;
    }

    return null;
  }
}
```

Here, we have implemented a simple `OCRService` class that uses the `image_picker` package to select an image from the gallery. Once the image is selected, we use the Firebase ML Vision API to process the image and extract the text.

## Using the OCR Service with GetX

Now, let's create a new GetX Controller to handle the OCR functionality and integrate it with our UI. Inside the `controllers` directory, create a new file called `ocr_controller.dart` with the following code:

```dart
import 'package:get/get.dart';
import 'package:your_app/services/ocr_service.dart';

class OCRController extends GetxController {
  final OCRService _ocrService = OCRService();
  final RxString extractedText = ''.obs;

  Future<void> extractText() async {
    final String? text = await _ocrService.extractTextFromImage();
    if (text != null) {
      extractedText.value = text;
    } else {
      // Handle error or cancellation
    }
  }
}
```

In the above code, we have created an `OCRController` class that uses the `OCRService` to extract text from the selected image. We use a `RxString` from GetX to hold the extracted text, which will automatically update the UI when the value changes.

## Integrating with the UI

Finally, let's integrate our OCR functionality with the UI. In your desired screen or widget, create a button or any other trigger to initiate the text extraction process:

```dart
class MyScreen extends StatelessWidget {
  final OCRController _ocrController = Get.put(OCRController());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('OCR Example'),
      ),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          ElevatedButton(
            onPressed: _ocrController.extractText,
            child: Text('Extract Text'),
          ),
          Obx(() => Text(_ocrController.extractedText.value)),
        ],
      ),
    );
  }
}
```

In this code snippet, we create a simple screen with a button that triggers the text extraction process when pressed. The extracted text is displayed using the `Obx` widget from GetX, which automatically updates the UI when the value of `extractedText` changes.

## Conclusion

In this tutorial, we have learned how to implement OCR and text extraction in a Flutter application using the GetX package. By leveraging the Firebase ML Vision API and the image_picker package, we were able to extract text from images and display it in our app. OCR opens up a world of possibilities for digitizing and extracting information from various sources in your applications. Happy coding!

## #Flutter #GetX #OCR #TextExtraction
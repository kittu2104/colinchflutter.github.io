---
layout: post
title: "Implementing image annotation and markup in a Flutter application"
description: " "
date: 2023-09-29
tags: [flutter, imageannotation, markup]
comments: true
share: true
---

Flutter is a popular framework for building cross-platform mobile applications. With its rich set of widgets and powerful UI capabilities, Flutter enables developers to create visually appealing and interactive apps. In this article, we will explore how to implement image annotation and markup functionality in a Flutter application.

## Getting Started

To begin, make sure you have Flutter installed on your machine. If not, [install Flutter](https://flutter.dev/docs/get-started/install) and set up your development environment.

## Setting up the Project

First, create a new Flutter project by running the following command in your terminal:

```bash
flutter create image_annotation_app
```

Change to the project directory:

```bash
cd image_annotation_app
```

## Adding Dependencies

Next, we need to add the necessary dependencies for image annotation and markup. Open the `pubspec.yaml` file and add the following lines:

```yaml
dependencies:
  flutter:
    sdk: flutter
  image_picker: ^0.8.4+2
  photo_view: ^0.11.1
  draw_it: ^2.0.0
```

Save the file and run the following command to fetch the new dependencies:

```bash
flutter pub get
```

## Building the UI

Now let's create the user interface for image annotation and markup. Open the `lib/main.dart` file and replace its contents with the following code:

```dart
import 'dart:io';

import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';
import 'package:photo_view/photo_view.dart';
import 'package:draw_it/draw_it.dart';

void main() {
  runApp(ImageAnnotationApp());
}

class ImageAnnotationApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Image Annotation App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: ImageAnnotationPage(),
    );
  }
}

class ImageAnnotationPage extends StatefulWidget {
  @override
  _ImageAnnotationPageState createState() => _ImageAnnotationPageState();
}

class _ImageAnnotationPageState extends State<ImageAnnotationPage> {
  File? _imageFile;

  Future<void> _getImage() async {
    final pickedFile = await ImagePicker().pickImage(source: ImageSource.gallery);
    if (pickedFile != null) {
      setState(() {
        _imageFile = File(pickedFile.path);
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Image Annotation'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Expanded(
              child: _imageFile != null
                  ? Container(
                      child: PhotoView(
                        imageProvider: FileImage(_imageFile!),
                      ),
                    )
                  : Text('No image selected'),
            ),
            ElevatedButton(
              onPressed: _getImage,
              child: Text('Select Image'),
            ),
            if (_imageFile != null)
              DrawIt(
                file: _imageFile!,
                options: DrawItOptions(
                  strokeWidth: 5.0,
                  strokeColor: Colors.red,
                ),
              ),
          ],
        ),
      ),
    );
  }
}
```

In this code, we create a Flutter application with a basic user interface. We use the `image_picker` package to allow the user to pick an image from their gallery. The selected image is displayed using the `photo_view` package. We also utilize the `draw_it` package to enable annotation and markup functionality on the image.

## Testing the App

Save the file and run the app on your preferred device or emulator:

```bash
flutter run
```

The app will launch and display a button to select an image from the gallery. Once an image is selected, it will be shown in a zoomable view. You can now annotate and markup the image using your finger on the screen.

## Conclusion

In this tutorial, we have learned how to implement image annotation and markup functionality in a Flutter application. We leveraged popular packages like `image_picker`, `photo_view`, and `draw_it` to achieve our goal. With this knowledge, you can enhance your Flutter apps by allowing users to annotate and markup images, opening up possibilities for various use cases such as educational apps, image editing tools, and more.

#flutter #imageannotation #markup
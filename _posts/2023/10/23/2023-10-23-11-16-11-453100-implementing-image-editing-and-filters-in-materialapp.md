---
layout: post
title: "Implementing image editing and filters in MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In today's digital age, image editing has become a crucial part of various applications, ranging from social media platforms to photo-sharing apps. With the help of the MaterialApp library in Flutter, we can easily implement image editing functionalities and apply filters to enhance images.

## Table of Contents
- [Getting Started](#getting-started)
- [Adding Image Editing Features](#adding-image-editing-features)
- [Applying Filters](#applying-filters)
- [Conclusion](#conclusion)

## Getting Started

To begin, make sure you have Flutter installed on your machine. If not, visit the [Flutter website](https://flutter.dev/) for installation instructions. Once you have Flutter set up, create a new project using the following command:

```flutter create image_editing_app```

Navigate into your project directory:

```cd image_editing_app```

Open the project in your preferred code editor, and in the `lib` folder, open `main.dart`.

## Adding Image Editing Features

To start implementing image editing features, import the necessary packages at the top of the file:

```dart
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';
import 'dart:io';
```

Next, create a class called `ImageEditingApp` that extends the `StatefulWidget` class:

```dart
class ImageEditingApp extends StatefulWidget {
  @override
  _ImageEditingAppState createState() => _ImageEditingAppState();
}
```

Inside the `_ImageEditingAppState` class, add the necessary variables and methods, including an `ImagePicker` instance to select an image from the device's file system:

```dart
class _ImageEditingAppState extends State<ImageEditingApp> {
  File _image;

  final picker = ImagePicker();
  
  Future<void> _getImage() async {
    final pickedImage = await picker.getImage(source: ImageSource.gallery);
    setState(() {
      if (pickedImage != null) {
        _image = File(pickedImage.path);
      } else {
        print('No image selected.');
      }
    });
  }
  
  // TODO: Implement image editing features
  
  // TODO: Implement filter functionality
  
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Image Editing App'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              if (_image != null)
                Image.file(_image),
              RaisedButton(
                child: Text('Select Image'),
                onPressed: _getImage,
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

## Applying Filters

To add filter functionality to your application, you can use the `flutter_image_filters` package. Add the package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_image_filters: ^0.1.3
```

Import the `flutter_image_filters` package:

```dart
import 'package:flutter_image_filters/flutter_image_filters.dart';
```

Inside the `_ImageEditingAppState` class, add a method that applies a filter to the selected image:

```dart
Future<void> _applyFilter(Filter filterType) async {
  if (_image != null) {
    final result = await FlutterImageFilters.applyFilter(
      filterType,
      _image.path,
    );
    setState(() {
      _image = File(result);
    });
  }
}
```

Now, you can add buttons for different filter types in the `build` method:

```dart
Column(
  mainAxisAlignment: MainAxisAlignment.center,
  children: [
    //... Image and select image button code here
    RaisedButton(
      child: Text('Apply Filter'),
      onPressed: () {
        _applyFilter(Filter.sepia);
      },
    ),
    RaisedButton(
      child: Text('Apply Filter'),
      onPressed: () {
        _applyFilter(Filter.grayscale);
      },
    ),
    // Add more filter buttons as needed
  ],
),
```

## Conclusion

By following these steps, you can easily implement image editing features and apply filters using the MaterialApp library in Flutter. Experiment with different filters and explore the capabilities of image editing functionalities to enhance your app's user experience.

Remember to experiment with different filter options and adjust the code according to your specific requirements.

# References
- [Flutter Documentation](https://flutter.dev/)
- [Flutter Image Filters package](https://pub.dev/packages/flutter_image_filters)
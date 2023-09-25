---
layout: post
title: "Implementing responsive image cropping using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [imagecropping]
comments: true
share: true
---

In this tech blog post, we will explore how to implement responsive image cropping using the `MediaQuery` class in Flutter. Image cropping is an essential aspect of many mobile applications, especially those dealing with user-uploaded images or displaying images in different aspect ratios.

## What is MediaQuery in Flutter?

`MediaQuery` is a class in Flutter that provides information about the current media (e.g., screen) properties. It allows you to query the device's screen size, orientation, and other attributes.

## Steps to implement responsive image cropping

1. Import the necessary dependencies:
```dart
import 'package:flutter/material.dart';
import 'package:image_cropper/image_cropper.dart';
```
2. Create a `Container` widget to hold the image:
```dart
Container(
  child: Image.network(
    'https://example.com/image.jpg',
    fit: BoxFit.cover,
  ),
)
```
3. Use a `GestureDetector` widget to handle the user's interaction with the image:
```dart
GestureDetector(
  onTap: () {
    _cropImage(); // Call the image cropping function
  },
  child: Container(
    child: Image.network(
      'https://example.com/image.jpg',
      fit: BoxFit.cover,
    ),
  ),
)
```
4. Define the `cropImage` function:
```dart
Future<void> _cropImage() async {
  final pickedFile = await ImagePicker().getImage(source: ImageSource.gallery);

  if (pickedFile == null) return; // No image selected

  final croppedFile = await ImageCropper.cropImage(
    sourcePath: pickedFile.path,
    aspectRatio: CropAspectRatio(ratioX: 1, ratioY: 1), // Set the desired aspect ratio
    compressQuality: 100, // Adjust the compression quality (0-100)
    maxWidth: 800, // Set the maximum width of the cropped image
    maxHeight: 800, // Set the maximum height of the cropped image
  );

  if (croppedFile != null) {
    // Handle the cropped image here
  }
}
```
5. Finally, wrap the image in a `MediaQuery` widget to make it responsive:
```dart
LayoutBuilder(
  builder: (BuildContext context, BoxConstraints constraints) {
    final screenWidth = constraints.maxWidth;
    final screenHeight = constraints.maxHeight;

    return MediaQuery(
      data: MediaQuery.of(context).copyWith(size: Size(screenWidth, screenHeight)),
      child: GestureDetector(
        onTap: () {
          _cropImage(); // Call the image cropping function
        },
        child: Container(
          child: Image.network(
            'https://example.com/image.jpg',
            fit: BoxFit.cover,
          ),
        ),
      ),
    );
  },
)
```

That's it! You have successfully implemented responsive image cropping using `MediaQuery` in Flutter. This approach ensures that the image maintains its aspect ratio and fits within the screen regardless of the device's orientation or size.

Remember to import the necessary dependencies and customize the function according to your project's requirements.

#flutter #imagecropping
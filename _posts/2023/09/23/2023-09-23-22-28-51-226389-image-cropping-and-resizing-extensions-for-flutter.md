---
layout: post
title: "Image cropping and resizing extensions for Flutter"
description: " "
date: 2023-09-23
tags: [imagecropper, imagepicker]
comments: true
share: true
---

Images are an integral part of many mobile app designs, and sometimes you need more control over how they are displayed. Flutter, a popular cross-platform framework, offers several extensions and packages that can help you crop and resize images effortlessly. In this article, we will explore some of the top image cropping and resizing extensions for Flutter.

## 1. ImageCropper

![flutter](https://example.com/images/flutter.png) #flutter #imagecropper

**ImageCropper** is a powerful Flutter package that allows you to crop images in various shapes, such as square, circle, or custom shapes. It provides a simple API to crop images and supports features like rotation, scaling, and aspect ratio adjustment. With ImageCropper, you can easily integrate a cropping functionality into your Flutter app and enhance the user experience.

To use ImageCropper, you need to add the following dependency to your `pubspec.yaml` file:

```dart
dependencies:
  image_cropper: ^1.3.1
```

Here's an example of how to crop an image with ImageCropper:

```dart
import 'package:image_cropper/image_cropper.dart';
import 'package:flutter/material.dart';
import 'dart:io';

class ImageCropScreen extends StatelessWidget {
  final File imageFile;

  ImageCropScreen(this.imageFile);

  @override
  Widget build(BuildContext context) {
    return FutureBuilder<File>(
      future: ImageCropper.cropImage(
        sourcePath: imageFile.path,
        aspectRatioPresets: [
          CropAspectRatioPreset.square,
          CropAspectRatioPreset.ratio3x2,
          CropAspectRatioPreset.original,
          CropAspectRatioPreset.ratio4x3,
          CropAspectRatioPreset.ratio16x9
        ],
        androidUiSettings: AndroidUiSettings(
            toolbarTitle: 'Crop Image',
            toolbarColor: Colors.deepOrange,
            toolbarWidgetColor: Colors.white,
            initAspectRatio: CropAspectRatioPreset.original,
            lockAspectRatio: false),
        iosUiSettings: IOSUiSettings(
          minimumAspectRatio: 1.0,
          lockAspectRatio: false,
        ),
      ),
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.done && snapshot.data != null) {
          return Image.file(snapshot.data);
        } else {
          return Center(child: CircularProgressIndicator());
        }
      },
    );
  }
}
```

## 2. ImagePicker

![flutter](https://example.com/images/flutter.png) #flutter #imagepicker

**ImagePicker** is another handy package that enables you to select images from the device's gallery or capture new ones using the camera. It also provides the ability to resize images before displaying or uploading them. With ImagePicker, you can choose an image, obtain its file path, and resize it according to your requirements.

To use ImagePicker, you need to add the following dependency to your `pubspec.yaml` file:

```dart
dependencies:
  image_picker: ^0.8.4+3
```

Here's an example of how to pick an image and resize it using ImagePicker:

```dart
import 'dart:io';
import 'package:image_picker/image_picker.dart';
import 'package:image/image.dart' as img;

resizeImage(String imagePath, int targetWidth, int targetHeight) {
  final imageFile = File(imagePath);
  img.Image image = img.decodeImage(imageFile.readAsBytesSync())!;
  img.Image resizedImage = img.copyResize(image,
      width: targetWidth, height: targetHeight);

  final resizedImagePath = imagePath.replaceAll('.jpg', '_resized.jpg');
  final resizedFile = File(resizedImagePath);
  resizedFile.writeAsBytesSync(img.encodeJpg(resizedImage));

  return resizedFile;
}

Future<File?> pickAndResizeImage(BuildContext context) async {
  final picker = ImagePicker();
  final pickedImage = await picker.pickImage(source: ImageSource.gallery);

  if (pickedImage != null) {
    final resizedImage = resizeImage(pickedImage.path, 300, 300);
    return resizedImage;
  }

  return null;
}
```

In the above example, we use the `ImagePicker` package to select an image from the device's gallery. Then we use the `image` package to resize the image to a target width and height. The resized image is saved as a new file, and its path is returned for further usage.

These are just two examples of the many image cropping and resizing extensions available for Flutter. Depending on your specific requirements, you can explore more packages and extensions to find the one that best suits your needs.
---
layout: post
title: "Image cropping and resizing extensions for Flutter"
description: " "
date: 2023-09-22
tags: [imageprocessing]
comments: true
share: true
---

When working with images in your Flutter application, you may come across the need to crop or resize images dynamically. Cropping and resizing images can be useful for various purposes, such as profile picture editing, thumbnail creation, or optimizing images for different device resolutions. In this blog post, we will explore some popular image cropping and resizing extensions for Flutter that can simplify this task for you.

## 1. `image_cropper` Extension

The [`image_cropper`](https://pub.dev/packages/image_cropper) package provides a simple and efficient way to crop images in your Flutter app. It supports both iOS and Android platforms and offers several cropping options. With this extension, you can select an image from the gallery or capture one using the camera, and then crop it to the desired size and aspect ratio.

### How to use `image_cropper`:

1. Add the `image_cropper` package to your `pubspec.yaml` file:

```dart
dependencies:
  image_cropper: ^<latest_version>
```

2. Import the package in your Dart file:

```dart
import 'package:image_cropper/image_cropper.dart';
```

3. Use the `ImageCropper.cropImage()` method to open the cropping UI and provide the image to be cropped:

```dart
File croppedImage = await ImageCropper.cropImage(
    sourcePath: imagePath, // The path of the image to be cropped
    aspectRatioPresets: [
        CropAspectRatioPreset.square,
        CropAspectRatioPreset.ratio16x9,
        CropAspectRatioPreset.original,
    ],
    androidUiSettings: AndroidUiSettings(
        toolbarTitle: 'Crop Image',
        toolbarColor: Colors.deepOrange,
        toolbarWidgetColor: Colors.white,
        initAspectRatio: CropAspectRatioPreset.original,
        lockAspectRatio: false,
    ),
    iosUiSettings: IOSUiSettings(
        title: 'Crop Image',
    ),
);
```

The `ImageCropper.cropImage()` method returns a `File` object containing the cropped image.

## 2. `flutter_image_compress` Extension

The [`flutter_image_compress`](https://pub.dev/packages/flutter_image_compress) package allows you to resize images in Flutter while maintaining their quality. Resizing images can help optimize their size and reduce the network bandwidth required for loading them. This extension supports both iOS and Android platforms and provides several options for resizing images.

### How to use `flutter_image_compress`:

1. Add the `flutter_image_compress` package to your `pubspec.yaml` file:

```dart
dependencies:
  flutter_image_compress: ^<latest_version>
```

2. Import the package in your Dart file:

```dart
import 'package:flutter_image_compress/flutter_image_compress.dart';
```

3. Use the `compress()` method to resize the image:

```dart
Uint8List compressedImage = await FlutterImageCompress.compressWithFile(
    imagePath, // The path of the image to be resized
    minWidth: 400,
    minHeight: 400,
    quality: 90,
    rotate: 180,
);
```

The `compress()` method returns a `Uint8List` containing the resized image data.

## Conclusion

Image cropping and resizing are common tasks in Flutter app development. The `image_cropper` and `flutter_image_compress` extensions provide efficient and easy-to-use solutions for achieving these tasks. By using these extensions, you can enhance the user experience and optimize the size of images in your Flutter applications.

#flutter #imageprocessing #mobileappdevelopment
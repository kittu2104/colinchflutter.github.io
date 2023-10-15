---
layout: post
title: "Popular Flutter plugins for image cropping and resizing"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---

When developing a Flutter application that involves working with images, image cropping and resizing are common tasks. Thankfully, there are several popular Flutter plugins available that make these tasks easier. In this blog post, we will explore two such plugins: `image_picker` and `image_cropper`.

## 1. image_picker

[image_picker](https://pub.dev/packages/image_picker) is a widely used Flutter plugin that allows users to pick images from their device's gallery or capture new images using the camera. It provides a simple API to retrieve the selected image and handle the necessary permissions.

To get started with `image_picker`, you need to add it as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  image_picker: ^0.8.4+2
```

Next, import the package in your Flutter code:

```dart
import 'package:image_picker/image_picker.dart';
```

To pick an image from the gallery, you can use the `ImagePicker.pickImage` method:

```dart
final pickedFile = await ImagePicker().pickImage(source: ImageSource.gallery);

if (pickedFile != null) {
  // Process the picked image
}
```

Similarly, you can capture a new image using the camera by specifying `ImageSource.camera` as the source.

## 2. image_cropper

[image_cropper](https://pub.dev/packages/image_cropper) is a powerful Flutter plugin that allows users to crop images before using them in their application. It provides a customizable cropping interface and supports a variety of cropping options, including aspect ratio, maximum and minimum dimensions, and more.

To integrate `image_cropper` into your Flutter project, add it as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  image_cropper: ^1.4.1
```

Import the package:

```dart
import 'package:image_cropper/image_cropper.dart';
```

To open the cropping interface and allow users to crop an image, you can use the `ImageCropper.cropImage` method:

```dart
File croppedFile = await ImageCropper.cropImage(
  sourcePath: file.path,
  aspectRatio: CropAspectRatio(ratioX: 1, ratioY: 1),
  compressQuality: 100,
  maxWidth: 500,
  maxHeight: 500,
);
```

In the example above, we specify the `sourcePath` as the path of the image file to be cropped. We also set an aspect ratio of 1:1, a maximum width and height of 500 pixels, and a compress quality of 100 (no compression).

These two popular Flutter plugins, `image_picker` and `image_cropper`, provide powerful and convenient features for working with images in your Flutter applications. By leveraging these plugins, you can easily implement image cropping and resizing functionality, enhancing the user experience of your app.

Useful resources:

- [image_picker on pub.dev](https://pub.dev/packages/image_picker)
- [image_cropper on pub.dev](https://pub.dev/packages/image_cropper)
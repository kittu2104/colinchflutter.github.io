---
layout: post
title: "Implementing image cropping functionality in Flutter"
description: " "
date: 2023-09-29
tags: []
comments: true
share: true
---

Image cropping is a common requirement in many mobile applications, especially those involving image editing or profile picture selection. In this blog post, we will explore how to implement image cropping functionality in Flutter using the `image_cropper` package.

## Getting Started

To get started, you'll need to set up a Flutter project and include the `image_cropper` package in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  image_cropper: ^1.4.1
```

Next, run the following command to fetch the package:

```bash
flutter pub get
```

## Implementing the Image Cropper

1. Import the required libraries:

```dart
import 'package:flutter/material.dart';
import 'package:image_cropper/image_cropper.dart';
import 'package:image_picker/image_picker.dart';
```

2. Add a button to select an image from the device:

```dart
class ImageCropperPage extends StatelessWidget {
  Future<void> _pickImage(ImageSource source) async {
    final picker = ImagePicker();
    final pickedImage = await picker.getImage(source: source);

    if (pickedImage != null) {
      _cropImage(File(pickedImage.path));
    }
  }

  Future<void> _cropImage(File image) async {
    final croppedImage = await ImageCropper.cropImage(
      sourcePath: image.path,
      aspectRatio: CropAspectRatio(ratioX: 1, ratioY: 1),
      maxWidth: 512,
      maxHeight: 512,
    );

    if (croppedImage != null) {
      // Do something with the cropped image
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Image Cropper'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            RaisedButton(
              onPressed: () => _pickImage(ImageSource.camera),
              child: Text('Take a Photo'),
            ),
            SizedBox(height: 12),
            RaisedButton(
              onPressed: () => _pickImage(ImageSource.gallery),
              child: Text('Choose from Gallery'),
            ),
          ],
        ),
      ),
    );
  }
}
```

In the above code, we use the `ImagePicker` package to select an image from either the camera or the gallery. The selected image is then passed to the `cropImage` method, where we define the cropping parameters using `ImageCropper.cropImage()`. Once the image is cropped, you can perform further actions with the cropped image.

## Conclusion

Implementing image cropping functionality in your Flutter application can be achieved easily using the `image_cropper` package. By following the steps mentioned above, you can enable users to select and crop images with ease.
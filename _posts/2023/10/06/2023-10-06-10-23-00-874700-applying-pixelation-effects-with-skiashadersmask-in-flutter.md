---
layout: post
title: "Applying pixelation effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

If you want to apply pixelation effects to your images in Flutter, you can use the `SkiaShadersMask` package. `SkiaShadersMask` is a powerful library that enables you to create various image effects by leveraging Skia Graphics Library.

In this tutorial, we will walk through the process of applying pixelation effects using `SkiaShadersMask` in Flutter. Let's get started!

## Prerequisites
Before we begin, make sure you have Flutter installed on your machine. You will also need to have a basic understanding of Flutter and Dart programming.

## Installation
To use the `SkiaShadersMask` package in your Flutter project, add it to your `pubspec.yaml` file:

```dart
dependencies:
  flutter:
    sdk: flutter
  skia_shaders_mask: ^1.0.0
```

After adding the dependency, run `flutter pub get` to fetch the package.

## Applying pixelation effects

### Step 1: Import required packages
First, import the necessary packages in your Dart file:

```dart
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';
import 'package:skia_shaders_mask/skia_shaders_mask.dart';
```

### Step 2: Create a widget
Next, create a widget that allows users to select an image and apply the pixelation effect:

```dart
class PixelationWidget extends StatefulWidget {
  @override
  _PixelationWidgetState createState() => _PixelationWidgetState();
}

class _PixelationWidgetState extends State<PixelationWidget> {
  ImagePicker _imagePicker = ImagePicker();
  ImageProvider? _imageProvider;
  double _pixelSize = 15.0;

  Future<void> _pickImage() async {
    final pickedFile = await _imagePicker.pickImage(source: ImageSource.gallery);
    if (pickedFile != null) {
      setState(() {
        _imageProvider = FileImage(File(pickedFile.path));
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Pixelation Effects')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: _pickImage,
              child: Text('Select Image'),
            ),
            SizedBox(height: 20.0),
            if (_imageProvider != null)
              Container(
                width: 300.0,
                height: 300.0,
                child: SkiaShadersMask(
                  imageProvider: _imageProvider!,
                  shader: PixelationShader(_pixelSize),
                ),
              ),
            if (_imageProvider == null)
              Text('No image selected'),
          ],
        ),
      ),
    );
  }
}
```

### Step 3: Apply the pixelation effect
In the `_PixelationWidgetState` class, we have added a `SkiaShadersMask` widget that wraps the selected image and applies the pixelation effect. We pass the `PixelationShader` as the `shader` parameter.

```dart
if (_imageProvider != null)
  Container(
    width: 300.0,
    height: 300.0,
    child: SkiaShadersMask(
      imageProvider: _imageProvider!,
      shader: PixelationShader(_pixelSize),
    ),
  ),
```

### Step 4: Adjust pixel size
To change the intensity of the pixelation effect, we provide a slider that allows users to adjust the `pixelSize` value. You can customize this part according to your requirements.

### Conclusion
By following these steps, you can easily apply pixelation effects to your images in Flutter using `SkiaShadersMask`. This library provides a convenient way to create various image effects and enhance the visual appeal of your Flutter applications.

Remember to experiment with different pixel sizes to achieve the desired effect. Have fun coding!

## #Flutter #ImageEffects
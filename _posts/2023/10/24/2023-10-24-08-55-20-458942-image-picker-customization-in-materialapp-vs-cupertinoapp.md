---
layout: post
title: "Image picker customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [References]
comments: true
share: true
---

When developing a mobile application, you might need to allow users to pick images from their device's gallery or camera. In Flutter, there are two main ways to customize the image picker based on the native look and feel: using MaterialApp or CupertinoApp.

## The MaterialApp Approach

MaterialApp is the default material design implementation for Flutter apps. It provides a set of widgets that emulate the look and behavior of the Material Design guidelines. To customize the image picker within a MaterialApp, you can make use of the ImagePicker package.

First, add the ImagePicker package to your `pubspec.yaml` file:

```yaml
dependencies:
  image_picker: ^0.8.3+2
```

Then, in your Dart file, import the package:

```dart
import 'package:image_picker/image_picker.dart';
```

To use the image picker, you can create a function that opens the image picker and retrieve the selected image:

```dart
Future<void> _pickImage(BuildContext context) async {
  final image = await ImagePicker().getImage(source: ImageSource.gallery);
  
  if (image != null) {
    // Handle the selected image
  }
}
```

In this example, we are using the ImagePicker class from the image_picker package and invoking the `getImage` method with `ImageSource.gallery` as the source, which opens the device's image gallery for selecting an image. You can also use `ImageSource.camera` to open the device's camera.

## The CupertinoApp Approach

CupertinoApp is the default Cupertino design implementation for Flutter apps. It provides widgets that emulate the look and behavior of iOS apps. Similar to the MaterialApp approach, you can customize the image picker using the ImagePicker package within a CupertinoApp.

Follow the same steps outlined for MaterialApp to add the ImagePicker package and import it into your Dart file. The usage of the image picker remains the same:

```dart
Future<void> _pickImage(BuildContext context) async {
  final image = await ImagePicker().getImage(source: ImageSource.gallery);
  
  if (image != null) {
    // Handle the selected image
  }
}
```

The only difference is the visual representation of the image picker when using the CupertinoApp approach. The picker will follow the iOS style rather than the Material Design style.

## Conclusion

Both MaterialApp and CupertinoApp allow you to customize the image picker in your Flutter app. MaterialApp provides a Material Design look and feel, while CupertinoApp gives your app an iOS-inspired look. Choose the approach that aligns with your app's design requirements and target platform.

#References

- Flutter ImagePicker package: [pub.dev/packages/image_picker](https://pub.dev/packages/image_picker)
- Flutter MaterialApp class: [api.flutter.dev/flutter/material/MaterialApp-class.html](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- Flutter CupertinoApp class: [api.flutter.dev/flutter/cupertino/CupertinoApp-class.html](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
---
layout: post
title: "Image picker widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When it comes to developing mobile applications, choosing the right widget is crucial to ensure a seamless user experience. One important feature that many applications require is the ability to pick and display images from the user's device. In this blog post, we will compare the image picker widget in MaterialApp and CupertinoApp, two popular widget sets in Flutter.

## MaterialApp

MatApp is the default material design widget set in Flutter, which provides a set of widgets that follow the Material Design guidelines by Google. To implement an image picker widget in a MaterialApp, you can use the image_picker package available on pub.dev. 

First, you need to add the image_picker dependency to your `pubspec.yaml` file:

```dart
dependencies:
  image_picker: ^0.8.4+2
```

Then, you can import the package in your Dart file:

```dart
import 'package:image_picker/image_picker.dart';
```

To display an image picker widget, you can use the `ImagePicker` class provided by the package. Here's an example of how you can use it:

```dart
final ImagePicker _picker = ImagePicker();

Future<void> pickImage() async {
  final XFile? image = await _picker.pickImage(source: ImageSource.gallery);

  if (image != null) {
    // Display the picked image
  }
}
```

In this example, we instantiate an `ImagePicker` object and call the `pickImage` method with the desired `ImageSource` (in this case, we choose the image from the gallery). The `pickImage` method returns an `XFile` object representing the picked image.

## CupertinoApp

CupertinoApp, on the other hand, is the widget set that follows the iOS design guidelines, providing widgets with the Cupertino look and feel. To implement an image picker widget in a CupertinoApp, you can also use the image_picker package mentioned earlier.

The implementation in a CupertinoApp is very similar to that in a MaterialApp, with a few minor differences in the UI elements. Here's an example of using the image picker widget in a CupertinoApp:

```dart
final ImagePicker _picker = ImagePicker();

Future<void> pickImage() async {
  final XFile? image = await _picker.pickImage(source: ImageSource.gallery);

  if (image != null) {
    // Display the picked image
  }
}
```

As you can see, the code for using the image picker widget in a CupertinoApp is identical to that in a MaterialApp. The only difference lies in the visual appearance of the picker widget, which matches the iOS style.

## Conclusion

In summary, both MaterialApp and CupertinoApp provide a convenient way to implement an image picker widget in your Flutter application. The choice between the two depends on the design and target platform of your application. Whether you prefer the Material Design look or the iOS style, you can easily integrate the image picker widget by using the image_picker package.
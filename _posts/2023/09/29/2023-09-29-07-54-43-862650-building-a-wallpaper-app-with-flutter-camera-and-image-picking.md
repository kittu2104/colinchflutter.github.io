---
layout: post
title: "Building a wallpaper app with Flutter camera and image picking"
description: " "
date: 2023-09-29
tags: [WallpaperApp]
comments: true
share: true
---

In this blog post, we will learn how to build a wallpaper app using Flutter, integrating the camera and image picking functionalities. This app will allow users to take photos directly from their device camera or choose images from their gallery to set as wallpapers.

## Getting Started

To get started, make sure you have Flutter installed on your machine. Open your favorite code editor and create a new Flutter project. Replace the contents of the `lib/main.dart` file with the following code:

```dart
import 'dart:io';

import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Wallpaper App',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: WallpaperScreen(),
    );
  }
}

class WallpaperScreen extends StatefulWidget {
  @override
  _WallpaperScreenState createState() => _WallpaperScreenState();
}

class _WallpaperScreenState extends State<WallpaperScreen> {
  File? _image;
  final picker = ImagePicker();

  Future getImage(ImageSource source) async {
    final pickedFile = await picker.getImage(source: source);

    setState(() {
      if (pickedFile != null) {
        _image = File(pickedFile.path);
      } else {
        print('No image selected.');
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Wallpaper App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            _image != null
                ? Image.file(_image!)
                : Text('No image selected.'),
            ElevatedButton(
              onPressed: () => getImage(ImageSource.camera),
              child: Text('Take Photo'),
            ),
            ElevatedButton(
              onPressed: () => getImage(ImageSource.gallery),
              child: Text('Choose from Gallery'),
            ),
          ],
        ),
      ),
    );
  }
}
```

## Explanation

- We start by importing the necessary libraries, including `dart:io` and the `image_picker` package.
- We create a `WallpaperScreen` widget that is a stateful widget to hold the main functionality of our app.
- Inside the `WallpaperScreen` class, we define a `_image` variable of type `File?` to store the selected image.
- We create an instance of `ImagePicker` to use for selecting images from the camera or gallery.
- The `getImage` method is responsible for fetching the image either from the camera or the gallery and updating the state accordingly.
- In the `build` method, we create a basic UI with an image widget to display the selected image (if any), and two buttons: one to take a photo and another to choose from the gallery.
- The `onPressed` callback for each button calls the `getImage` method, passing the appropriate `ImageSource` (camera or gallery).

## Conclusion

In this tutorial, we learned how to build a wallpaper app using Flutter and integrating the camera and image picking functionalities. This app can serve as a great starting point for developing more advanced wallpaper apps with additional features. Feel free to experiment and enhance the app according to your requirements.

Let us know your thoughts in the comments! #Flutter #WallpaperApp
---
layout: post
title: "Implementing a custom photo filter editor with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [flutter, photofilter]
comments: true
share: true
---

In this tutorial, we will explore how to create a custom photo filter editor using Flutter's Custom Painter. We will build a simple application that allows users to upload an image, apply various filters to it, and save the edited image.

## Prerequisites
Before getting started, make sure you have the following:
- Flutter SDK installed
- Flutter IDE or editor (e.g. Android Studio, VS Code) set up

## Steps

### Step 1: Setting up the Flutter project
1. Create a new Flutter project by running the following command in your terminal:
```
flutter create photo_filter_editor
```
2. Open the project in your preferred IDE or editor.

### Step 2: Adding dependencies
1. Open the `pubspec.yaml` file in your Flutter project.
2. Add the following dependencies:
```yaml
dependencies:
  flutter:
    sdk: flutter
  image:
  photo_view:
```
3. Save the file and run `flutter pub get` to download the dependencies.

### Step 3: Creating the UI
1. In the project's `lib` folder, open the `main.dart` file.
2. Replace the existing code with the following:
```dart
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';
import 'package:photo_view/photo_view.dart';

void main() => runApp(PhotoFilterEditorApp());

class PhotoFilterEditorApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Photo Filter Editor',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: PhotoFilterEditor(),
    );
  }
}

class PhotoFilterEditor extends StatefulWidget {
  @override
  _PhotoFilterEditorState createState() => _PhotoFilterEditorState();
}

class _PhotoFilterEditorState extends State<PhotoFilterEditor> {
  final picker = ImagePicker();
  late ImageProvider _imageProvider;

  Future<void> _selectImage() async {
    final pickedFile = await picker.getImage(source: ImageSource.gallery);
    if (pickedFile != null) {
      setState(() {
        _imageProvider = FileImage(pickedFile);
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Photo Filter Editor'),
      ),
      body: Center(
        child: _imageProvider == null
            ? Text('No image selected')
            : PhotoView(
                imageProvider: _imageProvider,
              ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _selectImage,
        tooltip: 'Select Image',
        child: Icon(Icons.photo_library),
      ),
    );
  }
}
```

### Step 4: Applying filters
1. Update the `_selectImage` method in the `_PhotoFilterEditorState` class as follows:
```dart
Future<void> _selectImage() async {
  final pickedFile = await picker.getImage(source: ImageSource.gallery);
  if (pickedFile != null) {
    final editedImage = await ImageFilter.applyFiltersFromFile(pickedFile.path);
    setState(() {
      _imageProvider = MemoryImage(editedImage);
    });
  }
}
```
2. Save the changes and import the `image_filter` package at the top of the file:
```dart
import 'package:image_filter/image_filter.dart';
```
3. Run the application and select an image. Notice that the selected image is displayed using the `PhotoView` widget.

### Step 5: Saving the edited image
1. Add the `image_picker` package to the `pubspec.yaml` file:
```yaml
dependencies:
  # ...
  image_picker:
```
2. Update the `_selectImage` method to save the edited image:
```dart
Future<void> _selectImage() async {
  final pickedFile = await picker.getImage(source: ImageSource.gallery);
  if (pickedFile != null) {
    final editedImage = await ImageFilter.applyFiltersFromFile(pickedFile.path);
    final savedFile = await ImageFilter.saveImage(editedImage);
    if (savedFile != null) {
      setState(() {
        _imageProvider = FileImage(savedFile);
      });
    }
  }
}
```
3. Save the changes and import the `image_filter` package at the top of the file:
```dart
import 'package:image_filter/image_filter.dart';
```

Congratulations! You have successfully implemented a custom photo filter editor using Flutter's Custom Painter. You can now upload images, apply filters to them, and save the edited images. Feel free to enhance the app by adding more filter options or implementing additional features.

#flutter #photofilter
---
layout: post
title: "Creating a custom video trimming toolbar in Flutter"
description: " "
date: 2023-10-03
tags: [flutter, videoediting]
comments: true
share: true
---

In this tutorial, we will explore how to create a custom video trimming toolbar in Flutter, allowing users to trim and edit videos within your application. 

## Prerequisites

Before proceeding with this tutorial, make sure you have the following:

- Flutter SDK installed on your machine.
- A basic understanding of Flutter and Dart programming languages.

## Step 1: Setting up the Project

1. Create a new Flutter project using the following command:
```bash
flutter create video_trimming_toolbar
```
2. Open the project in your preferred code editor.

## Step 2: Adding Dependencies

In order to implement the video trimming functionality, we will need to add some dependencies to our Flutter project. Open the `pubspec.yaml` file and add the following dependencies under the `dependencies` section:
```yaml
dependencies:
  flutter:
    sdk: flutter
  video_trimmer: ^2.1.0
  file_picker: ^4.1.0
```
Save the file and run `flutter pub get` to fetch the newly added dependencies.

## Step 3: Building the Custom Trimming Toolbar

Now, let's start building our custom video trimming toolbar.

1. Create a new file called `trimming_toolbar.dart` and define a new class called `TrimmingToolbar`.
2. Import the required dependencies:
```dart
import 'package:flutter/material.dart';
import 'package:video_trimmer/video_trimmer.dart';
import 'package:file_picker/file_picker.dart';
```
3. Define a stateful widget called `TrimmingToolbar` that extends `StatefulWidget`.
```dart
class TrimmingToolbar extends StatefulWidget {
  @override
  _TrimmingToolbarState createState() => _TrimmingToolbarState();
}
```
4. Define the state class `_TrimmingToolbarState` that extends `State<TrimmingToolbar>`.
```dart
class _TrimmingToolbarState extends State<TrimmingToolbar> {
  // Add necessary variables and methods here
}
```
5. Implement the build method inside the `_TrimmingToolbarState` class to define the UI layout of the custom trimming toolbar:
```dart
@override
Widget build(BuildContext context) {
  return Container(
    // Build the UI layout of the trimming toolbar here
  );
}
```
6. Implement the necessary logic for trimming the video. You can use the `video_trimmer` package to handle the video trimming functionality. Here's an example of how you can integrate it into your custom trimming toolbar:
```dart
void _trimVideo() async {
  final Trimmer _trimmer = Trimmer();

  // Open file picker to select the video file
  FilePickerResult? result = await FilePicker.platform.pickFiles(
    type: FileType.custom,
    allowedExtensions: ['mp4'], // Specify the allowed video file extensions
  );

  if (result != null) {
    PlatformFile file = result.files.first;

    await _trimmer.loadVideo(videoFile: File(file.path));

    // Show the video trimmer interface and get the trimmed video file
    await _trimmer.showVideoTrimmer(context,
        videoEditCallback: (video, _) {
      // Handle the trimmed video file
    });
  }
}
```
7. Customize the UI layout of the trimming toolbar as per your requirements. Add buttons or controls for opening the video picker and invoking the trimming functionality.
8. Create an instance of `TrimmingToolbar` inside your application and place it wherever you want to display the custom video trimming toolbar.

## Step 4: Testing the Application

To test the application, run the following command in your terminal:
```bash
flutter run
```

The application will launch on your connected device or emulator. Use the custom video trimming toolbar to select and trim videos within your app.

Congratulations! You have successfully built a custom video trimming toolbar in Flutter.

#flutter #videoediting
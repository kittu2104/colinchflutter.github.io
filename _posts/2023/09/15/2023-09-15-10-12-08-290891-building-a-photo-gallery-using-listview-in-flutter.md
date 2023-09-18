---
layout: post
title: "Building a photo gallery using ListView in Flutter."
description: " "
date: 2023-09-15
tags: [photogallery]
comments: true
share: true
---

In this tutorial, we will learn how to create a photo gallery using the `ListView` widget in Flutter. Flutter is a UI toolkit for building beautiful, natively compiled applications for mobile, web, and desktop from a single codebase.

## Prerequisites
Before we start, make sure you have the following installed:
- Flutter SDK
- A code editor (such as Visual Studio Code or IntelliJ IDEA)
- Android or iOS emulator

## Step 1: Set Up Flutter Project
To begin, create a new Flutter project by running the following command in your terminal:
```
flutter create photo_gallery
```
Next, navigate to the project directory:
```
cd photo_gallery
```

## Step 2: Add Dependencies
Open the `pubspec.yaml` file and add the following dependencies:
```yaml
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
  cached_network_image: ^3.0.0
```
Save the file and run the following command to update the dependencies:
```
flutter pub get
```

## Step 3: Create Photo Model
In the `lib` directory, create a new file called `photo_model.dart`. Add the following code to define the `Photo` model:
```dart
class Photo {
  final String imageUrl;
  final String caption;

  Photo({required this.imageUrl, required this.caption});
}
```

## Step 4: Create Photo Data
Create a new file called `photo_data.dart` and add the following code to define a list of sample photos:
```dart
import 'photo_model.dart';

List<Photo> photos = [
  Photo(
    imageUrl: 'https://example.com/photo1.jpg',
    caption: 'Beautiful Sunset',
  ),
  Photo(
    imageUrl: 'https://example.com/photo2.jpg',
    caption: 'Mountain Landscape',
  ),
  Photo(
    imageUrl: 'https://example.com/photo3.jpg',
    caption: 'City Skyline',
  ),
];
```

## Step 5: Create Photo Item Widget
Now, let's create a new file called `photo_item_widget.dart` and add the following code to define the `PhotoItemWidget`:
```dart
import 'package:flutter/material.dart';
import 'photo_model.dart';

class PhotoItemWidget extends StatelessWidget {
  final Photo photo;

  const PhotoItemWidget({required this.photo});

  @override
  Widget build(BuildContext context) {
    return ListTile(
      leading: Image.network(photo.imageUrl),
      title: Text(photo.caption),
    );
  }
}
```

## Step 6: Build the Photo Gallery
In the `lib` directory, open the `main.dart` file and replace the default code with the following:
```dart
import 'package:flutter/material.dart';
import 'photo_data.dart';
import 'photo_item_widget.dart';

void main() {
  runApp(PhotoGalleryApp());
}

class PhotoGalleryApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Photo Gallery',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Photo Gallery'),
        ),
        body: ListView.builder(
          itemCount: photos.length,
          itemBuilder: (BuildContext context, int index) {
            return PhotoItemWidget(photo: photos[index]);
          },
        ),
      ),
    );
  }
}
```

## Step 7: Run the App
Save all files and run the app using the following command:
```
flutter run
```
Now, you should see a photo gallery with the sample photos displayed in a `ListView` on your emulator or device.

## Conclusion
In this tutorial, we learned how to create a photo gallery using the `ListView` widget in Flutter. Feel free to customize the UI or enhance the functionality according to your requirements. Happy coding!

#flutter #photogallery
---
layout: post
title: "Implementing responsive image zooming using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: []
comments: true
share: true
---

In Flutter, `MediaQuery` is a powerful tool that allows you to make your app responsive and adapt its layout and components based on the device's screen size and orientation. In this blog post, we will explore how to implement responsive image zooming using `MediaQuery` in Flutter.

## Step 1: Setting up the project

Start by creating a new Flutter project or opening an existing one. You can do this by running the following command in your terminal:

```
$ flutter create responsive_image_zoom
```

## Step 2: Adding dependencies

Open the `pubspec.yaml` file of your project and add the `photo_view` dependency. This package provides a zoomable image widget that we will use in our project.

```yaml
dependencies:
  flutter:
    sdk: flutter
  photo_view: ^0.9.2
```

Save the file and run the following command to fetch the new dependency:

```
$ flutter pub get
```

## Step 3: Implementing the responsive image zooming

Now, let's create a new Flutter widget and implement the responsive image zooming functionality. Start by creating a new file called `zoomable_image.dart` in your project's `lib` directory.

```dart
import 'package:flutter/material.dart';
import 'package:photo_view/photo_view.dart';
import 'package:flutter_screenutil/flutter_screenutil.dart';

class ZoomableImage extends StatelessWidget {
  final String imageUrl;

  const ZoomableImage({Key key, this.imageUrl}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Container(
      width: double.infinity,
      height: MediaQuery.of(context).size.height.h.toDouble(),
      child: PhotoView(
        imageProvider: NetworkImage(imageUrl),
        minScale: PhotoViewComputedScale.contained * 0.8,
        maxScale: PhotoViewComputedScale.covered * 1.8,
      ),
    );
  }
}
```

In the code above, we create a new `ZoomableImage` widget that takes an `imageUrl` as a parameter. Inside the `build` method, we use `MediaQuery` to set the height of the container to the full height of the screen. We then use the `PhotoView` widget from the `photo_view` package, which provides zooming functionality for images.

## Step 4: Implementing the image zooming screen

To use the `ZoomableImage` widget, let's create a new screen that displays an image and allows the user to zoom in and out. Open the `main.dart` file and replace its contents with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:responsive_image_zoom/zoomable_image.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Image Zoom',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: ZoomableImageScreen(),
    );
  }
}

class ZoomableImageScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Zoomable Image'),
      ),
      body: ZoomableImage(
        imageUrl: 'https://example.com/my-image.jpg',
      ),
    );
  }
}
```

In the code above, we create a new `ZoomableImageScreen` widget, which is the main screen of our app. Inside the `build` method, we display an `AppBar` with a title and set the body to the `ZoomableImage` widget we created earlier. Replace the `imageUrl` with the URL of the image you want to display.

## Step 5: Running the app

Save all the changes and run the app using the following command:

```
$ flutter run
```

This will launch the app on a simulator or connected device, and you should see a screen displaying the image you specified. You can now pinch to zoom in and out to view the image up close.

That's it! You have successfully implemented responsive image zooming using `MediaQuery` in Flutter. Play around with different images and device sizes to see the responsiveness in action.

## Conclusion

`MediaQuery` is a powerful tool in Flutter that allows you to create responsive layouts and components. By utilizing it, along with the `photo_view` package, we were able to easily implement image zooming functionality that adapts to different screen sizes and orientations.
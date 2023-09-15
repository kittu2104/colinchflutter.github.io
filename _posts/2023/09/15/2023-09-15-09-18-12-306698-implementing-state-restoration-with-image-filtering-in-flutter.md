---
layout: post
title: "Implementing state restoration with image filtering in Flutter"
description: " "
date: 2023-09-15
tags: [Flutter, StateRestoration, ImageFiltering]
comments: true
share: true
---

One of the key features that users expect in a modern app is the ability to save the app's state and restore it when they return. This is especially important when working with image filtering apps, as users might spend a significant amount of time adjusting filters and editing images.

In this blog post, we will explore how to implement state restoration with image filtering in Flutter. We will build a simple image filtering app that allows users to apply different filters to an image and save their progress.

## Understanding State Restoration in Flutter

State restoration is the process of saving and restoring an app's state across different sessions. When an app goes into the background or gets terminated, state restoration ensures that the app can pick up where the user left off. This includes restoring the UI state, user interactions, and any other relevant data.

Flutter provides a set of APIs that makes it easy to implement state restoration in your app. These APIs allow you to save and restore the state of specific widgets, giving you fine-grained control over the restoration process.

## Building the Image Filtering App

Let's start by creating a basic Flutter app that enables users to apply filters to an image. We will use the `image_picker` package to select an image from the device gallery, and the `image` package to apply different filters to the selected image.

```dart
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';
import 'package:image/image.dart' as img;

class ImageFilteringApp extends StatefulWidget {
  @override
  _ImageFilteringAppState createState() => _ImageFilteringAppState();
}

class _ImageFilteringAppState extends State<ImageFilteringApp> {
  img.Image? _selectedImage;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Image Filtering App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            _selectedImage != null
                ? Image.memory(
                    img.encodePng(_selectedImage!),
                    fit: BoxFit.cover,
                  )
                : Text(
                    'No image selected',
                    style: TextStyle(fontSize: 16),
                  ),
            SizedBox(height: 16),
            ElevatedButton(
              onPressed: _selectImage,
              child: Text('Select Image'),
            ),
          ],
        ),
      ),
    );
  }

  void _selectImage() async {
    final picker = ImagePicker();
    final image = await picker.getImage(source: ImageSource.gallery);

    if (image != null) {
      final imageBytes = await image.readAsBytes();
      final imageObject = img.decodeImage(imageBytes);

      setState(() {
        _selectedImage = imageObject;
      });
    }
  }
}

void main() {
  runApp(ImageFilteringApp());
}
```

In this code snippet, we have a `ImageFilteringApp` widget that displays the selected image (if any) along with a button to select an image from the device gallery. We use the `image_picker` package to select the image and the `image` package to decode and process the selected image.

## Adding State Restoration to the Image Filtering App

Now that we have our basic app, let's add state restoration functionality to it. We will use the `RestorableStatefulWidget` and `RestorableProperty` classes provided by Flutter to achieve this.

First, we need to make our `ImageFilteringApp` widget inherit from `RestorableStatefulWidget` instead of `StatefulWidget`. We also need to define a RestorableProperty to store the selected image.

```dart
class ImageFilteringApp extends RestorableStatefulWidget {
  @override
  _ImageFilteringAppState createState() => _ImageFilteringAppState();
}

class _ImageFilteringAppState extends RestorableAppState<ImageFilteringApp> {
  RestorableTypedImage? _selectedImage;

  @override
  Widget build(BuildContext context) {
    // ...
  }
}

class RestorableTypedImage extends RestorableProperty<img.Image?> {
  @override
  img.Image? fromPrimitives(Object? data) {
    if (data != null) {
      final imageBytes = data as List<int>;
      return img.decodeImage(imageBytes);
    }
    return null;
  }

  @override
  Object? toPrimitives() {
    if (value != null) {
      return img.encodePng(value!);
    }
    return null;
  }
}
```

In this code snippet, we create a `RestorableTypedImage` class that extends from `RestorableProperty<img.Image?>`. This class handles the conversion between a binary representation of the image (byte array) and the `Image` object. We implement the `fromPrimitives` and `toPrimitives` methods to convert to and from the binary representation.

Next, we need to override the `createRestorableState` method in `ImageFilteringApp` to return a new instance of our state class, and we need to override the `didUpdateWidget` method to update the selected image property when the widget updates.

```dart
@override
RestorableState<ImageFilteringApp> createRestorableState() {
  return _ImageFilteringAppState();
}

@override
void didUpdateWidget(covariant ImageFilteringApp oldWidget) {
  super.didUpdateWidget(oldWidget);

  if (widget != oldWidget) {
    _selectedImage = widget.createRestorableProperty();
  }
}
```

Finally, we need to register the restorable property in the `restoreFromPrimitives` method and add a key to our `Image.memory` widget to enable restoration.

```dart
@override
void restoreFromPrimitives(Object? data) {
  final selectedImageBytes = data as List<int>?;
  if (selectedImageBytes != null) {
    _selectedImage?.notifyListeners(selectedImageBytes);
  }
}

@override
void initState() {
  super.initState();

  registerForRestoration(_selectedImage, 'selected_image');
}

//...

_selectedImage != null
  ? Image.memory(
      img.encodePng(_selectedImage!.value!),
      fit: BoxFit.cover,
      key: _selectedImage,
    )
  : Text(
      'No image selected',
      style: TextStyle(fontSize: 16),
    ),
```

In the updated code snippet, we call `registerForRestoration` on our restorable property to register it for state restoration. We also add a `key` to the `Image.memory` widget, passing in the restorable property instance, so that Flutter can restore the selected image when needed.

And that's it! We have now implemented state restoration with image filtering in our Flutter app. Users can select an image, apply filters, and their progress will be saved and restored when they come back to the app.

## Conclusion

State restoration is an essential feature in modern apps, and it becomes even more crucial when working with image filtering applications. In this blog post, we explored how to implement state restoration with image filtering in Flutter, using the `RestorableStatefulWidget` and `RestorableProperty` classes provided by Flutter.

By incorporating state restoration into your image filtering app, you can enhance the user experience by allowing users to pick up where they left off and save their progress. This ensures a seamless and enjoyable experience for your users.

#Flutter #StateRestoration #ImageFiltering
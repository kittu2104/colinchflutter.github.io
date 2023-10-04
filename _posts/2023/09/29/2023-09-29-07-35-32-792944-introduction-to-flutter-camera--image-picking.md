---
layout: post
title: "Introduction to Flutter Camera & Image Picking"
description: " "
date: 2023-09-29
tags: [camera, imagepicker]
comments: true
share: true
---

## Setting Up the Packages

To get started, you will need to add the camera and image_picker packages to your Flutter project. Open your `pubspec.yaml` file and add the following dependencies:

```dart
dependencies:
  camera: ^0.9.0+2
  image_picker: ^0.8.4+2
```

After adding the dependencies, run `flutter pub get` to install the packages.

## Using the Camera Package

The camera package provides a robust set of APIs to access the camera functionality in Flutter. Let's see how to incorporate it into your app.

Import the camera package in your Dart file:

```dart
import 'package:camera/camera.dart';
```

Next, initialize the camera by calling the `availableCameras()` method. This method returns a list of available cameras on the device. You can choose the desired camera by specifying its index (typically 0 for the rear camera or 1 for the front camera):

```dart
List<CameraDescription> cameras;

Future<void> initializeCamera() async {
  cameras = await availableCameras();
}

```

To open the camera preview, create a `CameraController` instance and pass in the selected camera. Then, call the `initialize()` method on the controller:

```dart
CameraController controller;

Future<void> openCamera() async {
  controller = CameraController(cameras[0], ResolutionPreset.high);
  await controller.initialize();
}
```

Finally, simply display the camera output using the `CameraPreview` widget:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text('Camera Preview'),
    ),
    body: CameraPreview(controller),
  );
}
```

By following these steps, you can display the camera preview in your Flutter app. However, capturing photos and saving them to the device requires more code. To learn more about advanced features like capturing images using the camera package, refer to the package's documentation.

## Using the Image Picker Package

The image_picker package allows you to easily select images from the device's gallery or capture photos using the camera. Let's see how to utilize it.

Import the image_picker package in your Dart file:

```dart
import 'package:image_picker/image_picker.dart';
```

To select an image from the gallery, use the `getImage()` method:

```dart
PickedFile pickedFile;

Future<void> pickImageFromGallery() async {
  pickedFile = await ImagePicker().getImage(source: ImageSource.gallery);
}
```

To capture a photo using the camera, use the `getImage()` method with `source: ImageSource.camera`:

```dart
Future<void> captureImage() async {
  pickedFile = await ImagePicker().getImage(source: ImageSource.camera);
}
```

Once you have selected an image or captured a photo, you can display it in your app using the `Image` widget:

```dart
@override
Widget build(BuildContext context) {
  return Column(
    children: [
      ElevatedButton(
        onPressed: pickImageFromGallery,
        child: Text('Select Image'),
      ),
      ElevatedButton(
        onPressed: captureImage,
        child: Text('Capture Photo'),
      ),
      pickedFile != null
          ? Image.file(File(pickedFile.path))
          : Container(),
    ],
  );
}
```

With the help of the image_picker package, you can easily enable image picking and camera functionality in your Flutter app.

## Conclusion

Integrating camera and image picking features into your Flutter app is essential for building richer and more interactive experiences. The camera and image_picker packages provide convenient APIs to implement these functionalities. By following the steps outlined in this blog post, you can leverage these packages to create powerful camera and image handling capabilities in your Flutter application.

#flutter #camera #imagepicker
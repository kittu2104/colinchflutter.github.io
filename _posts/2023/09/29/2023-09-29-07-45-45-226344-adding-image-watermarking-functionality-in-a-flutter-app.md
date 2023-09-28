---
layout: post
title: "Adding image watermarking functionality in a Flutter app"
description: " "
date: 2023-09-29
tags: [flutter, watermarking]
comments: true
share: true
---

With more and more people sharing images online, it's important to protect your images from unauthorized use. One way to help protect your images is by adding watermarks. In this tutorial, we will explore how to add image watermarking functionality in a Flutter app.

## 1. Adding Dependencies

To get started, we need to add the required dependencies to our `pubspec.yaml` file:

```dart
dependencies:
  flutter:
    sdk: flutter
  image_editor:
  permission_handler:
  image_picker:
  path_provider:
```

- The `image_editor` package provides the necessary functionalities to edit the images.
- The `permission_handler` package is used to request and check for permissions required to access the gallery and save images.
- The `image_picker` package allows us to pick images from the device's gallery.
- The `path_provider` package helps in getting the directory path to save the watermarked image.

Remember to run `flutter pub get` in your terminal to fetch the newly added dependencies.

## 2. Creating a Watermark Overlay Widget

Let's create a new `WatermarkOverlayWidget` that will be used to overlay a watermark on the selected image.

```dart
class WatermarkOverlayWidget extends StatelessWidget {
  final String watermarkText;
  final Uint8List imageBytes;

  WatermarkOverlayWidget({
    required this.watermarkText,
    required this.imageBytes,
  });

  @override
  Widget build(BuildContext context) {
    return Stack(
      children: [
        Image.memory(imageBytes), // Display the selected image
        Positioned(
          bottom: 16,
          right: 16,
          child: Opacity(
            opacity: 0.7,
            child: Text(
              watermarkText,
              style: TextStyle(
                fontSize: 24,
                fontWeight: FontWeight.bold,
                color: Colors.white,
              ),
            ),
          ),
        ),
      ],
    );
  }
}
```

This widget takes in the watermark text and the bytes of the selected image and overlays the watermark at the bottom right corner of the image.

## 3. Adding Watermark Functionality

Now, let's integrate the watermarking functionality into our Flutter app. We'll create a `WatermarkPage` widget that allows users to select an image and add a watermark to it.

```dart
class WatermarkPage extends StatefulWidget {
  const WatermarkPage({Key? key}) : super(key: key);

  @override
  _WatermarkPageState createState() => _WatermarkPageState();
}

class _WatermarkPageState extends State<WatermarkPage> {
  String? watermarkText;
  Uint8List? imageBytes;

  void _pickImage() async {
    // TODO: Implement image picking using image_picker package
    // Make sure to check for permissions beforehand
  }

  void _saveWatermarkedImage() async {
    // TODO: Implement saving watermarked image using image_editor and path_provider packages
    // Make sure to check for permissions beforehand
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Watermark App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: _pickImage,
              child: Text('Pick Image'),
            ),
            if (imageBytes != null)
              WatermarkOverlayWidget(
                watermarkText: watermarkText ?? '',
                imageBytes: imageBytes!,
              ),
            SizedBox(height: 16),
            if (imageBytes != null && watermarkText != null)
              ElevatedButton(
                onPressed: _saveWatermarkedImage,
                child: Text('Save Watermarked Image'),
              ),
          ],
        ),
      ),
    );
  }
}
```

The `WatermarkPage` widget displays a button to pick an image, and if an image is selected, it will show the selected image with an overlay watermark. Finally, there is an additional button to save the watermarked image.

## Conclusion

In this tutorial, we've explored how to add image watermarking functionality in a Flutter app. By following these steps, you can now protect your images by adding watermarks. Remember to handle permissions and implement the necessary functionality for image picking and saving to complete the app.

#flutter #watermarking
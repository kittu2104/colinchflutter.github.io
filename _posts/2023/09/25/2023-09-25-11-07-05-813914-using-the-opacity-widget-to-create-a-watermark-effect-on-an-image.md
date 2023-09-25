---
layout: post
title: "Using the Opacity widget to create a watermark effect on an image"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---
## Adding a subtle watermark with Flutter

In this tutorial, we'll explore how to use the Opacity widget in Flutter to create a watermark effect on an image. Watermarks are commonly used to protect digital content or add branding to images. By reducing the opacity of the watermark, we can make it appear more subtle and less intrusive.

Let's get started by creating a new Flutter project and importing the necessary dependencies.

## Setting up the project

Open your terminal and create a new Flutter project:

```bash
$ flutter create watermark_app
$ cd watermark_app
```

Update the `pubspec.yaml` file to include the `image_picker` package:

```yaml
dependencies:
  flutter:
    sdk: flutter
  image_picker: ^0.8.4+4
```

Save the file and run `flutter pub get` to download the dependencies.

## Creating the watermark effect

1. Open the `lib/main.dart` file and remove the default code.

2. Import the required packages:

```dart
import 'dart:io';
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';
```

3. Create a stateful widget called `WatermarkApp`:

```dart
void main() => runApp(WatermarkApp());

class WatermarkApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Watermark App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: WatermarkScreen(),
    );
  }
}
```

4. Create a stateful widget called `WatermarkScreen`:

```dart
class WatermarkScreen extends StatefulWidget {
  @override
  _WatermarkScreenState createState() => _WatermarkScreenState();
}

class _WatermarkScreenState extends State<WatermarkScreen> {
  File? _image;

  Future<void> _pickImage() async {
    final picker = ImagePicker();
    final pickedImage = await picker.pickImage(source: ImageSource.gallery);
    if (pickedImage != null) {
      setState(() {
        _image = File(pickedImage.path);
      });
    }
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
            if (_image != null) ...[
              Image.file(_image!),
              SizedBox(height: 16.0),
              Opacity(
                opacity: 0.5,
                child: Text(
                  'Your Watermark',
                  style: TextStyle(
                    fontSize: 24.0,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
            ] else ...[
              Text('No image selected.'),
            ],
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _pickImage,
        child: Icon(Icons.add),
      ),
    );
  }
}
```

In this example code, we use the `ImagePicker` package to allow the user to select an image from their device's gallery. When an image is selected, we set the `_image` state variable with the selected image. The selected image is then displayed using the `Image.file` widget. We also use the `Opacity` widget to add the watermark text with an opacity of 0.5.

5. Save the changes and run the app using the command `flutter run`.

## Conclusion

In this tutorial, we learned how to use the Opacity widget in Flutter to create a watermark effect on an image. We also explored how to use the ImagePicker package to select an image from the device's gallery. By adjusting the opacity of the watermark, we can control its visibility and make it appear more subtle.

Feel free to customize the watermark text and the opacity level to fit your requirements.
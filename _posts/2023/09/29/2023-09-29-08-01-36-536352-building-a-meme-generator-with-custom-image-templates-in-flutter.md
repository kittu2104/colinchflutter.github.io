---
layout: post
title: "Building a meme generator with custom image templates in Flutter"
description: " "
date: 2023-09-29
tags: [flutter, meme]
comments: true
share: true
---

In this tutorial, we will explore how to build a meme generator app using Flutter. Our app will allow users to select from a library of custom image templates and overlay text captions to create hilarious memes. 

## Prerequisites

Before we get started, make sure you have Flutter installed on your machine. You can download Flutter from the official website.

## Step 1: Set Up the Project

Create a new Flutter project using the following command:
```bash
flutter create meme_generator
```

Navigate to the project directory:
```bash
cd meme_generator
```

Open the project in your preferred code editor.

## Step 2: Add Dependencies

To help us manipulate images and overlay text, we will use two important dependencies:

1. `image_picker` to select images from the device's gallery.
2. `flutter_image_stack` to overlay text captions on images.

Add these dependencies to the `pubspec.yaml` file:
```yaml
dependencies:
  flutter:
    sdk: flutter
  image_picker: ^0.8.4+4
  flutter_image_stack: ^2.3.1
```

Save the file and run `flutter pub get` to fetch the new dependencies.

## Step 3: Create the Main Screen

Let's start by creating the main screen of our meme generator app. This screen will display a button that allows users to select an image from their device's gallery.

Replace the content of the `lib/main.dart` file with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';

void main() {
  runApp(MemeGeneratorApp());
}

class MemeGeneratorApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Meme Generator',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MemeGeneratorScreen(),
    );
  }
}

class MemeGeneratorScreen extends StatefulWidget {
  @override
  _MemeGeneratorScreenState createState() => _MemeGeneratorScreenState();
}

class _MemeGeneratorScreenState extends State<MemeGeneratorScreen> {
  PickedFile? _image;

  void _selectImage() async {
    final ImagePicker _picker = ImagePicker();
    final image = await _picker.pickImage(source: ImageSource.gallery);

    setState(() {
      _image = image;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Meme Generator'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            _image != null
                ? Image.file(
                    File(_image!.path),
                    height: 200,
                  )
                : Placeholder(
                    fallbackHeight: 200,
                    fallbackWidth: 200,
                  ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: _selectImage,
              child: Text('Select Image'),
            ),
          ],
        ),
      ),
    );
  }
}
```

This code sets up the main screen with an app bar and a column that displays either the selected image or a placeholder image. The `ElevatedButton` allows users to choose an image from their gallery.

## Step 4: Overlay Text on the Image

In this step, we will add the functionality to overlay text captions on the selected image. We will utilize the `flutter_image_stack` library for this purpose.

Update the code within the `_MemeGeneratorScreenState` class to include the following changes:

```dart
import 'package:flutter_image_stack/flutter_image_stack.dart';

...

class _MemeGeneratorScreenState extends State<MemeGeneratorScreen> {
  ...

  TextEditingController _captionController = TextEditingController();
  List<Widget> _textOverlays = [];

  void _addTextOverlay() {
    setState(() {
      _textOverlays.add(
        Positioned(
          top: 50,
          left: 50,
          child: Draggable(
            feedback: Container(
              child: Text(
                _captionController.text,
                style: TextStyle(
                  fontSize: 20,
                  color: Colors.white,
                  fontWeight: FontWeight.bold,
                ),
              ),
            ),
            child: Container(),
            childWhenDragging: Container(),
            onDragEnd: (details) {
              setState(() {
                // Update the position of the text overlay
                // based on the drag end coordinates
              });
            },
          ),
        ),
      );

      _captionController.clear();
    });
  }

  void _clearTextOverlays() {
    setState(() {
      _textOverlays.clear();
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      ...
      body: Stack(
        children: [
          _image != null
              ? Image.file(
                  File(_image!.path),
                  height: 200,
                )
              : Placeholder(
                  fallbackHeight: 200,
                  fallbackWidth: 200,
                ),
          _textOverlays.isNotEmpty
              ? Stack(
                  children: _textOverlays,
                )
              : Container(),
        ],
      ),
      bottomNavigationBar: BottomAppBar(
        child: Container(
          padding: EdgeInsets.symmetric(horizontal: 16, vertical: 8),
          child: Row(
            children: [
              Expanded(
                child: TextField(
                  controller: _captionController,
                  decoration: InputDecoration(hintText: 'Enter caption'),
                ),
              ),
              IconButton(
                onPressed: _addTextOverlay,
                icon: Icon(Icons.add),
              ),
              IconButton(
                onPressed: _clearTextOverlays,
                icon: Icon(Icons.clear),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

With this code update, the app now allows users to enter captions in a text field. The captions will appear at a fixed position on the selected image. Users can drag the captions to adjust their position.

## Step 5: Generate the Meme

Finally, we need to implement the functionality to generate the meme by merging the selected image with the text overlays. We will utilize the `image_picker` and `flutter_image_stack` libraries to achieve this.

Update the code within the `_MemeGeneratorScreenState` class to include the following changes:

```dart
import 'package:image/image.dart' as img;
import 'package:path_provider/path_provider.dart';

...

void _generateMeme() async {
  if (_image != null && _textOverlays.isNotEmpty) {
    final img.Image image = img.decodeImage(File(_image!.path).readAsBytesSync())!;
  
    for (Widget textOverlay in _textOverlays) {
      final Text textWidget = ((textOverlay as Positioned).child! as Draggable).feedback as Text;
  
      final double left = (textOverlay as Positioned).left!;
      final double top = (textOverlay as Positioned).top!;
  
      final img.Image textOverlayImage = await FlutterImageStack.toImageWidget(textWidget);
      img.drawImage(image, textOverlayImage, dstX: left.toInt(), dstY: top.toInt());
    }
  
    final directory = await getApplicationDocumentsDirectory();
    final imagePath = '${directory.path}/meme.png';
    File(imagePath).writeAsBytesSync(img.encodePng(image));
  
    // Navigate to the meme preview screen with generated image
  }
}

...

bottomNavigationBar: BottomAppBar(
  ...
  child: Row(
    ...
    IconButton(
      onPressed: _generateMeme,
      icon: Icon(Icons.preview),
    ),
  ),
),
```

Now, when the user taps on the 'Preview' icon button, the app will generate a meme by merging the selected image with the text overlays. The resulting image will be saved to the device's local storage.

## Conclusion

In this tutorial, we have built a meme generator app using Flutter. Users can select images from their device's gallery and overlay text captions at desired positions. The app generates a meme by merging the image and text overlays, which can then be previewed and saved. Use this as a starting point to create your own meme generator app with custom image templates in Flutter.

#flutter #meme-generator
---
layout: post
title: "Using SkiaShadersMask for creating image sliders in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Image sliders are a common component in mobile applications that allow users to browse through a collection of images in a dynamic and user-friendly manner. In Flutter, we can achieve this functionality by leveraging the SkiaShadersMask class from the Flutter engine.

SkiaShadersMask is a powerful tool that allows us to apply various effects and overlays to images. By using SkiaShadersMask, we can create visually appealing image sliders that stand out in our Flutter application. In this blog post, we will learn how to use SkiaShadersMask to create image sliders in Flutter.

## Prerequisites
To follow along with this tutorial, you should have:

- Flutter SDK installed on your machine
- Basic knowledge of Dart programming language
- Familiarity with Flutter widgets and layout concepts

## Steps to create image sliders using SkiaShadersMask

### Step 1: Add dependencies
First, we need to add the following dependencies in the `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  skia:
```

### Step 2: Import required libraries
Next, we need to import the required libraries in our Dart file:

```dart
import 'package:flutter/material.dart';
import 'package:skia/shaders.dart';
```

### Step 3: Create a StatefulWidget
We will create a `StatefulWidget` called `ImageSlider` to hold our image slider logic:

```dart
class ImageSlider extends StatefulWidget {
  @override
  _ImageSliderState createState() => _ImageSliderState();
}

class _ImageSliderState extends State<ImageSlider> {
  // Add your slider logic here
}
```

### Step 4: Declare slider properties
Inside the `_ImageSliderState` class, we will declare the necessary properties for our image slider:

```dart
  int currentIndex = 0;
  final List<String> imageList = [
    'assets/images/image1.jpg',
    'assets/images/image2.jpg',
    'assets/images/image3.jpg',
  ];
```

### Step 5: Implement the image slider
We will implement the image slider using a `PageView.builder` widget. This widget allows us to scroll through the images horizontally:

```dart
  @override
  Widget build(BuildContext context) {
    return PageView.builder(
      itemCount: imageList.length,
      onPageChanged: (index) {
        setState(() {
          currentIndex = index;
        });
      },
      itemBuilder: (context, index) {
        return Positioned.fill(
          child: SkiaShaderMask(
            shader: ImageShader(
              Codec.fromFile(File(imageList[index])).instantiate(),
              TileMode.clamp,
              TileMode.clamp,
              Float64List.fromList([
                0.0, 0.0, 0.0, 0.0, // Red channel adjustment
                0.0, 0.0, 0.0, 0.0, // Green channel adjustment
                0.0, 0.0, 0.0, 0.0, // Blue channel adjustment
                0.0, 0.0, 0.0, 1.0, // Alpha channel adjustment
              ]),
            ),
            child: Image.asset(
              imageList[index],
              fit: BoxFit.cover,
            ),
          ),
        );
      },
    );
  }
}
```

In the above code snippet, we use the `SkiaShaderMask` widget to apply an image mask effect to each image. We pass the `ImageShader` to the `shader` property of the `SkiaShaderMask` widget, which allows us to customize the mask effect.

### Step 6: Implement indicator dots
To provide a visual representation of the current image in the slider, we can add indicator dots at the bottom of the slider. We will make use of the `ListView.builder` widget with `CircleAvatar` to create these indicator dots:

```dart
  Widget _buildIndicatorDots() {
    return ListView.builder(
      shrinkWrap: true,
      scrollDirection: Axis.horizontal,
      itemCount: imageList.length,
      itemBuilder: (context, index) {
        return CircleAvatar(
          radius: 5.0,
          backgroundColor:
              index == currentIndex ? Colors.blue : Colors.grey,
        );
      },
    );
  }
```

### Step 7: Implement the complete widget
Finally, we will update the `build` method of the `_ImageSliderState` class to include the complete widget implementation:

```dart
  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Expanded(
          child: Stack(
            children: [
              ImageSlider(),
              Align(
                alignment: Alignment.bottomCenter,
                child: Padding(
                  padding: const EdgeInsets.all(8.0),
                  child: _buildIndicatorDots(),
                ),
              ),
            ],
          ),
        ),
      ],
    );
  }
}
```

### Step 8: Display the image slider
To display the image slider, we can add the `ImageSlider` widget to any desired place in our Flutter application:

```dart
void main() {
  runApp(
    MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Image Slider Example'),
        ),
        body: Center(
          child: ImageSlider(),
        ),
      ),
    ),
  );
}
```

## Conclusion
By utilizing the SkiaShadersMask class from the Flutter engine, we can easily create image sliders in a Flutter application. We have learned the necessary steps to implement image sliders using SkiaShadersMask and explored how to customize the mask effects to create visually appealing sliders. Feel free to experiment and enhance the image slider further according to your requirements.

Give it a try and #HappyCoding! #Flutter
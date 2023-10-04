---
layout: post
title: "Using GetX for image manipulation and filters in Flutter"
description: " "
date: 2023-09-29
tags: [GetX, imageManipulation, imageFilters]
comments: true
share: true
---

Flutter, the popular cross-platform development framework, offers a wide range of tools and packages to simplify the development process. One such package is GetX, a powerful state management and dependency injection solution. In this article, we will explore how to utilize GetX for image manipulation and applying filters in a Flutter application.

## Installing GetX

Before we start, make sure to add the GetX package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  get: ^4.6.1 # Version may vary
```

Then, run `flutter packages get` from the terminal to install the package.

## Loading and Displaying an Image

To begin, let's load and display an image on the screen using the `GetX` package. We'll assume you already have a basic Flutter project set up.

First, import the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';
```

Create a `GetX` controller to manage the state of the image:

```dart
class ImageController extends GetxController {
  final image = ''.obs;
  
  void loadImage(String imagePath) {
    image.value = imagePath;
  }
}
```

Within your main widget, create an instance of the `ImageController`:

```dart
class MyApp extends StatelessWidget {
  final ImageController _imageController = Get.put(ImageController());
  
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      // ... rest of the MaterialApp setup
    );
  }
}
```

Now, let's display the image:

```dart
class MyApp extends StatelessWidget {
  final ImageController _imageController = Get.put(ImageController());
  
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: Obx(() => _imageController.image.value.isNotEmpty
              ? Image.network(_imageController.image.value)
              : CircularProgressIndicator(),
          ),
        ),
      ),
    );
  }
}
```

When you call the `loadImage()` function in the `ImageController`, the displayed image will automatically update.

## Applying Image Filters

Now that we can display an image, let's explore how to apply filters using GetX. For this example, we will use the **flutter_color_filter** package.

First, add the package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_color_filter: any
```

Then, import the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';
import 'package:flutter_color_filter/flutter_color_filter.dart';
```

Next, modify the `ImageController` class to include filter functionality:

```dart
class ImageController extends GetxController {
  final image = ''.obs;
  final filter = ColorFilter.identity().obs;
  
  void loadImage(String imagePath) {
    image.value = imagePath;
  }
  
  void applyFilter(ColorFilter newFilter) {
    filter.value = newFilter;
  }
}
```

Within your widget, add a dropdown menu to select the desired filter:

```dart
DropdownButton<ColorFilter>(
  value: _imageController.filter.value,
  onChanged: (newValue) => _imageController.applyFilter(newValue),
  items: [
    DropdownMenuItem(
      value: ColorFilter.matrix(<double>[
        0.2126, 0.7152, 0.0722, 0, 0,
        0.2126, 0.7152, 0.0722, 0, 0,
        0.2126, 0.7152, 0.0722, 0, 0,
        0,      0,      0,      1, 0,
      ]),
      child: Text('Grayscale'),
    ),
    DropdownMenuItem(
      value: ColorFilter.matrix(<double>[
        1,  0,  0, 0, 0,
        0,  0.9, 0, 0, 0,
        0,  0,  0.8, 0, 0,
        0,  0,  0,   1, 0,
      ]),
      child: Text('Sepia'),
    ),
  ],
)
```

Finally, update the `Image.network` widget to include the filter:

```dart
Image.network(
  _imageController.image.value,
  color: _imageController.filter.value,
  colorBlendMode: BlendMode.color,
)
```

With these modifications, you can now select different filters from the dropdown menu and apply them to the displayed image.

## Conclusion

In this article, we have explored how to utilize the GetX package in Flutter for image loading, displaying, and applying filters. GetX's powerful state management and reactive nature make it an excellent choice for handling images and their manipulations efficiently.

#flutter #GetX #imageManipulation #imageFilters
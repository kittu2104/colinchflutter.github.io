---
layout: post
title: "Implementing responsive image filters using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [Flutter, ResponsiveDesign]
comments: true
share: true
---

In today's digital world, responsive design has become a crucial aspect of developing user-friendly and visually appealing applications. One aspect of responsive design is applying image filters based on the screen size or device orientation. In this article, we will explore how to implement responsive image filters using the powerful `MediaQuery` class in Flutter.

## What is `MediaQuery`?

`MediaQuery` is a Flutter class that provides information about the current app's media, including the device screen size, orientation, brightness, and more. It allows developers to build dynamic and responsive UIs based on device-specific properties.

## Adding dependencies

To get started, add the following dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_svg: ^0.22.0
  image:
```

Make sure to run `flutter pub get` to fetch the latest packages.

## Implementing responsive image filters

1. Import the required dependencies.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';
```

2. Create a simple stateful widget.

```dart
class ResponsiveImageFilter extends StatefulWidget {
  @override
  _ResponsiveImageFilterState createState() => _ResponsiveImageFilterState();
}
```

3. Define the `_ResponsiveImageFilterState` class.

```dart
class _ResponsiveImageFilterState extends State<ResponsiveImageFilter> {
  double _blurAmount = 0.0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Image Filter'),
      ),
      body: Center(
        child: MediaQuery.of(context).size.width >= 600
            ? _buildFilteredBackground()
            : _buildOriginalBackground(),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          setState(() {
            _blurAmount = _blurAmount == 0.0 ? 10.0 : 0.0;
          });
        },
        child: Icon(Icons.blur_on),
      ),
    );
  }

  Widget _buildFilteredBackground() {
    return Container(
      color: Colors.grey[200],
      child: Image.asset(
        'assets/images/background_image.jpg',
        filterQuality: FilterQuality.low,
        color: Colors.black54,
        colorBlendMode: BlendMode.darken,
        fit: BoxFit.cover,
        alignment: Alignment.center,
        height: MediaQuery.of(context).size.height,
        width: MediaQuery.of(context).size.width * 0.5,
      ),
    );
  }

  Widget _buildOriginalBackground() {
    return Container(
      color: Colors.grey[200],
      child: SvgPicture.asset(
        'assets/images/background_image.svg',
        height: MediaQuery.of(context).size.height,
      ),
    );
  }
}
```

4. Update the `main.dart` file with the following code:

```dart
import 'package:flutter/material.dart';

import 'responsive_image_filter.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Image Filter',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: ResponsiveImageFilter(),
    );
  }
}
```

5. Add images to the `assets` folder. Create a new folder, `assets/images`, and place your `background_image.jpg` and `background_image.svg` files inside it.

6. Run your application:

```bash
flutter run
```

## Conclusion

By leveraging the power of `MediaQuery`, we have successfully implemented responsive image filters in a Flutter application. Now, when the app is displayed on larger screens, a blurred version of the background image is shown, providing a visually appealing experience. Don't hesitate to experiment and enhance your applications with responsive design techniques to engage your users. #Flutter #ResponsiveDesign
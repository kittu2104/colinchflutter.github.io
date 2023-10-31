---
layout: post
title: "Using SVG to create personalized avatars and profile pictures in Flutter"
description: " "
date: 2023-10-31
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to use SVG (Scalable Vector Graphics) to create personalized avatars and profile pictures in Flutter. SVG is a vector-based image format that allows for high-quality graphics and is scalable without losing any visual quality. Flutter provides a library called `flutter_svg` that allows us to render SVG images in our applications.

## Table of Contents

- Introduction to SVG
- Setting up the project
- Creating an AvatarWidget
- Generating personalized avatars
- Conclusion

## Introduction to SVG

SVG is an XML-based vector image format that can be rendered in web browsers and applications. It provides a powerful way to create and display graphics with sharp, smooth edges at any size or resolution. Unlike raster images (e.g., JPEG, PNG), SVG images are not pixel-based but mathematically described shapes, lines, and curves. This makes SVG images resolution-independent and ideal for creating personalized avatars and profile pictures.

## Setting up the project

To get started, create a new Flutter project and add the `flutter_svg` dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_svg: ^0.22.0
```

Run `flutter pub get` to install the dependency.

## Creating an AvatarWidget

Let's create a new `AvatarWidget` that will render the SVG image with optional customization options such as size and colors. 

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';

class AvatarWidget extends StatelessWidget {
  final String imagePath;
  final double size;
  final Color backgroundColor;
  final Color foregroundColor;

  AvatarWidget({
    required this.imagePath,
    this.size = 80,
    this.backgroundColor = Colors.white,
    this.foregroundColor = Colors.black,
  });

  @override
  Widget build(BuildContext context) {
    return CircleAvatar(
      radius: size / 2,
      backgroundColor: backgroundColor,
      child: SvgPicture.asset(
        imagePath,
        color: foregroundColor,
      ),
    );
  }
}
```

The `AvatarWidget` is a stateless widget that takes in the `imagePath`, `size`, `backgroundColor`, and `foregroundColor` as parameters. We use the `CircleAvatar` widget to create a circular shape for the avatar and set its radius based on the provided size. Inside the `CircleAvatar`, we use the `SvgPicture.asset` from the `flutter_svg` package to render the SVG image.

## Generating personalized avatars

Now that we have our `AvatarWidget` ready, we can use it to generate personalized avatars. Here's an example of how we can create avatars with different colors:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Avatar Demo',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Avatar Demo'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: [
              AvatarWidget(
                imagePath: 'assets/avatar.svg',
                size: 200,
                backgroundColor: Colors.yellow,
              ),
              AvatarWidget(
                imagePath: 'assets/avatar.svg',
                size: 150,
                backgroundColor: Colors.green,
              ),
              AvatarWidget(
                imagePath: 'assets/avatar.svg',
                size: 100,
                backgroundColor: Colors.blue,
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

Here, we create multiple instances of the `AvatarWidget` and customize them with different sizes and background colors. The `imagePath` points to the SVG image asset.

## Conclusion

In this tutorial, we explored how to use SVG to create personalized avatars and profile pictures in Flutter. By leveraging the `flutter_svg` package, we were able to render SVG images and customize their appearance. SVG provides a flexible and resolution-independent way to create high-quality graphics, making it a great choice for avatar generation in Flutter applications.
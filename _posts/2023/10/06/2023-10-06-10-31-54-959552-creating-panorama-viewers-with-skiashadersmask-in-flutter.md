---
layout: post
title: "Creating panorama viewers with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

## Introduction

Panorama viewers are a great way to display immersive 360-degree images or videos. In Flutter, you can create stunning panorama viewers using the SkiaShadersMask package. SkiaShadersMask provides a set of powerful tools for rendering images with custom shaders and masks.

In this tutorial, we will guide you through the process of creating a panorama viewer using SkiaShadersMask in Flutter.

## Prerequisites

Before we begin, make sure you have the following prerequisites:

- Flutter SDK installed on your machine
- A basic understanding of Flutter development

## Step 1: Install the SkiaShadersMask package

To get started, you need to add the SkiaShadersMask package to your Flutter project. Open your `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  skia_shaders_mask: ^1.0.0
```

Save the file and run `flutter pub get` in your terminal to download and install the package.

## Step 2: Create the panorama viewer widget

Next, let's create a new Flutter widget to display the panorama. Create a new file called `panorama_viewer.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:skia_shaders_mask/skia_shaders_mask.dart';

class PanoramaViewer extends StatelessWidget {
  final String imageUrl;

  PanoramaViewer({required this.imageUrl});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: ShaderMask(
        shaderCallback: (Rect bounds) {
          return Shader.maskFilter(
            ImageShader(UIImage(
              imageProvider: NetworkImage(imageUrl),
            )),
            MaskFilter.blur(BlurStyle.normal, 10),
          );
        },
        child: Image.network(imageUrl, fit: BoxFit.cover),
      ),
    );
  }
}
```

In the code above, we have defined a new `PanoramaViewer` widget that takes an `imageUrl` as a parameter. Inside the `build` method, we use the `ShaderMask` widget to apply a custom shader to the image. We create a `MaskFilter.blur` and use it as a mask for the `ImageShader` to blur the image.

## Step 3: Using the panorama viewer

To use the panorama viewer, simply instantiate the `PanoramaViewer` widget with the desired `imageUrl` and add it to your Flutter app. Here's an example of how you can use it:

```dart
import 'package:flutter/material.dart';
import 'package:your_app/panorama_viewer.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Panorama Viewer Example'),
        ),
        body: Center(
          child: PanoramaViewer(
            imageUrl: 'https://example.com/panorama.jpg',
          ),
        ),
      ),
    );
  }
}
```

In the code above, we import the `PanoramaViewer` widget and add it as the child of the `Center` widget. Replace the `imageUrl` with your own panorama image URL.

## Conclusion

Creating panorama viewers with SkiaShadersMask in Flutter is a powerful and straightforward process. By leveraging the SkiaShadersMask package, you can add custom shaders and masks to your images, resulting in stunning and immersive panorama viewers.

Remember to experiment with different shaders and masks to achieve the desired visual effects. Happy coding!

#flutter #panorama #viewer
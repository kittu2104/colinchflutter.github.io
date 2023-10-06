---
layout: post
title: "Creating background removal with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to create a background removal effect using the `SkiaShadersMask` class in Flutter. The `SkiaShadersMask` class allows us to apply custom shaders to mask an image or any other drawable. This can be useful in various scenarios, such as removing the background of an image or applying creative effects.

## Prerequisites

Before getting started, make sure you have the following:

- Flutter SDK installed on your system
- A basic understanding of Flutter and Dart programming language
- A code editor of your choice (e.g., Visual Studio Code, Android Studio, etc.)

## Step 1: Set up a new Flutter project

First, let's set up a new Flutter project by running the following command in your terminal:

```flutter create background_removal```

Once the project is created, navigate to the project directory:

```cd background_removal```

## Step 2: Add dependencies

Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  skia_shaders: any
```

Save the file and run the following command to fetch the dependencies:

```flutter pub get```

## Step 3: Create a new Flutter widget

In Flutter, UI elements are represented as widgets. We will create a new `BackgroundRemovalWidget` to encapsulate the background removal functionality. Create a new file named `background_removal_widget.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:skia_shaders/skia_shaders.dart';

class BackgroundRemovalWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      color: Colors.white,
      child: ShaderMask(
        shaderCallback: (Rect bounds) {
          return LinearGradient(
            colors: [
              Colors.transparent,
              Colors.black,
              Colors.black,
              Colors.transparent,
            ],
            stops: [0.0, 0.25, 0.75, 1.0],
          ).createShader(bounds);
        },
        blendMode: BlendMode.dstIn,
        child: Image.asset('assets/images/background_removal_example.jpg'),
      ),
    );
  }
}
```

In this code, we import the necessary packages and create a `BackgroundRemovalWidget` as a `StatelessWidget`. Inside the `build` method, we wrap the widget with a `Container` widget and set its `color` to `Colors.white`.

Then, we use the `ShaderMask` widget to apply a custom shader to our `Image` widget. We define the `shaderCallback` that generates a `LinearGradient` with transparent and black colors at different stops. This will create a mask effect that removes the background.

Finally, we set the `blendMode` to `BlendMode.dstIn` to specify how the image should be blended with the mask.

## Step 4: Update the main.dart file

Open the `lib/main.dart` file and update the `MyApp` class to use the `BackgroundRemovalWidget`. Replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

import 'background_removal_widget.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Background Removal Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Background Removal'),
        ),
        body: Center(
          child: BackgroundRemovalWidget(),
        ),
      ),
    );
  }
}
```

## Step 5: Run the app

Save the changes and run the app using the following command:

```flutter run```

You should now see the app running with the background removal effect applied to the image.

## Conclusion

In this tutorial, we have learned how to create a background removal effect using the `SkiaShadersMask` class in Flutter. This can be a powerful tool for creating engaging and visually appealing UI elements in your Flutter applications.

Feel free to experiment further with different shaders and blending modes to create unique effects tailored to your specific needs. Happy coding!

**#Flutter #BackgroundRemoval**
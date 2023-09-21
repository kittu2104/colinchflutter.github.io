---
layout: post
title: "How to create a custom hero shape using CustomClipper in Flutter"
description: " "
date: 2023-09-21
tags: [flutter, customshape]
comments: true
share: true
---

Flutter provides a lot of flexibility when it comes to customizing the user interface. One way to create a unique and eye-catching UI is by using custom shapes. In this tutorial, we'll learn how to create a custom hero shape using `CustomClipper` in Flutter.

## Step 1: Create a new Flutter project

First, let's create a new Flutter project by running the following command:

```
flutter create custom_hero_shape
```

## Step 2: Update the project dependencies

Next, open the `pubspec.yaml` file and update the `dependencies` section as follows:

```
dependencies:
  flutter:
    sdk: flutter
  flutter_svg: ^0.22.0
```

Save the file and run the following command to fetch the updated dependencies:

```
flutter pub get
```

## Step 3: Create a custom shape

In this step, we'll create a custom shape for the hero widget. To do this, we'll create a new file called `custom_shape.dart` in the `lib` directory and add the following code:

```dart
import 'package:flutter/material.dart';

class CustomHeroShape extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    final path = Path();
    path.moveTo(0, size.height * 0.5);
    path.quadraticBezierTo(
        size.width * 0.25, size.height * 0.4, size.width * 0.5, 0);
    path.quadraticBezierTo(
        size.width * 0.75, size.height * 0.4, size.width, size.height * 0.5);
    path.lineTo(size.width, size.height);
    path.lineTo(0, size.height);
    path.close();
    return path;
  }

  @override
  bool shouldReclip(covariant CustomClipper<Path> oldClipper) {
    return false;
  }
}
```

In the code above, we're extending the `CustomClipper` class and overriding the `getClip` method to define our custom shape using a series of `quadraticBezierTo` and `lineTo` commands.

## Step 4: Implement the custom hero shape

Now, let's implement the custom hero shape in our Flutter app. Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';

import 'custom_shape.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom Hero Shape',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Hero Shape'),
      ),
      body: Center(
        child: Hero(
          tag: 'custom_hero',
          child: ClipPath(
            clipper: CustomHeroShape(),
            child: SvgPicture.asset(
              'assets/custom_svg.svg',
              width: 200,
              height: 200,
            ),
          ),
        ),
      ),
    );
  }
}
```

In the code above, we're using the `ClipPath` widget to apply the `CustomHeroShape` clipper to the `SvgPicture` widget. The `Hero` widget is used to create a hero animation between two screens.

## Step 5: Add the SVG asset

To complete the example, let's add a custom SVG asset. Create an `assets` folder in the `lib` directory and place an SVG file named `custom_svg.svg` inside it.

## Step 6: Test the app

Finally, let's test our app by running the following command:

```
flutter run
```

You should see a screen with a custom hero shape applied to the SVG image. When the hero animation is triggered, the image should transition smoothly between screens.

That's it! You've successfully created a custom hero shape using `CustomClipper` in Flutter.

#flutter #customshape
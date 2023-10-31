---
layout: post
title: "Creating mobile-friendly animations with SVG in Flutter"
description: " "
date: 2023-10-31
tags: []
comments: true
share: true
---

In this blog post, we will explore how to create mobile-friendly animations using Scalable Vector Graphics (SVG) in Flutter. SVG is a vector-based image format that allows us to define graphics with XML-based code and scale them without losing quality. Flutter is a powerful UI framework that enables us to develop cross-platform apps with native performance and flexibility. By combining the power of SVG and Flutter, we can create visually appealing and responsive animations for our mobile applications.

## Table of Contents

1. Introduction to SVG and Flutter
2. Setting up the Flutter project
3. Using the `flutter_svg` package
4. Importing SVG assets
5. Animating SVG elements
6. Creating responsive animations
7. Conclusion

## 1. Introduction to SVG and Flutter

Scalable Vector Graphics (SVG) is a widely supported image format that allows us to create resolution-independent graphics for the web. It uses XML-based code to define shapes, paths, and styles, making it highly customizable and flexible. On the other hand, Flutter is an open-source UI framework developed by Google that allows us to build beautiful and fast applications using a single codebase for multiple platforms.

## 2. Setting up the Flutter project

To get started, make sure you have Flutter installed on your system. You can check Flutter's official documentation for installation instructions. Once Flutter is installed, create a new Flutter project using the following command:

```shell
flutter create svg_animations
```

Navigate into the project directory:

```shell
cd svg_animations
```

Open the project in your preferred code editor.

## 3. Using the `flutter_svg` package

Flutter provides a package called `flutter_svg` that allows us to render SVG images in our Flutter applications. To add the `flutter_svg` package to your project, open the `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter_svg: ^0.22.0
```

Save the changes and run the following command to fetch and install the package:

```shell
flutter pub get
```

## 4. Importing SVG assets

To use SVG assets in our Flutter project, we need to place the SVG files in the `assets` directory. Create a new directory called `assets` in the project root if it doesn't already exist. Copy your SVG files into this directory.

Next, open the `pubspec.yaml` file and add the following lines under the `flutter` section:

```yaml
flutter:
  assets:
    - assets/
```

Save the changes and run the following command to update the project dependencies:

```shell
flutter pub get
```

Now we can use these SVG assets in our Flutter application.

## 5. Animating SVG elements

To animate SVG elements in Flutter, we can leverage Flutter's built-in animation framework. We can use the `AnimationController` class to control the animation and the `Tween` class to define the animation's values. By combining these two classes, we can create smooth and interactive animations.

First, let's import the necessary packages in our Flutter application:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';
```

Next, let's create a simple animation that scales an SVG image. In the `build` method of our widget, define an `AnimationController` and a `Tween`:

```dart
AnimationController _scaleController;
Animation<double> _scaleAnimation;

@override
void initState() {
  _scaleController = AnimationController(
    vsync: this,
    duration: Duration(seconds: 1),
  );

  _scaleAnimation = Tween<double>(begin: 1, end: 2).animate(_scaleController);

  _scaleController.repeat(reverse: true);

  super.initState();
}
```

In the `build` method, use the `SvgPicture.asset` widget to display the SVG image and apply the animation:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    body: Center(
      child: ScaleTransition(
        scale: _scaleAnimation,
        child: SvgPicture.asset(
          'assets/my_svg_image.svg',
          width: 200,
          height: 200,
        ),
      ),
    ),
  );
}
```

This will create a continuous scaling animation on the SVG image.

## 6. Creating responsive animations

To make our SVG animations responsive, we can use Flutter's layout widgets such as `MediaQuery` and `LayoutBuilder`. By utilizing these widgets, we can adapt the animations based on the available screen size.

For example, let's say we want our SVG image to scale based on the width of the screen. We can modify the above code as follows:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    body: Center(
      child: LayoutBuilder(
        builder: (context, constraints) {
          final screenWidth = constraints.maxWidth;
          final targetWidth = 200;

          final scaleFactor = screenWidth / targetWidth;

          return ScaleTransition(
            scale: _scaleAnimation.drive(Tween<double>(
              begin: 1,
              end: 2 * scaleFactor,
            )),
            child: SvgPicture.asset(
              'assets/my_svg_image.svg',
              width: targetWidth,
              height: targetWidth,
            ),
          );
        },
      ),
    ),
  );
}
```

With this modification, the SVG image will scale proportionally based on the width of the screen.

## 7. Conclusion

In this blog post, we’ve learned how to create mobile-friendly animations using SVG in Flutter. By combining the power of SVG graphics and Flutter's animation framework, we can create visually appealing and responsive animations in our mobile applications. SVG animations can enhance the user experience and bring our apps to life. Experiment with different SVG assets and animation techniques to create engaging and interactive user interfaces.

By using Flutter's `flutter_svg` package, importing SVG assets, and implementing animations with Flutter's animation framework, we can achieve smooth and visually pleasing animations in our Flutter applications. With responsive design techniques, we can ensure our animations adapt to different screen sizes.

We hope this blog post has given you a good understanding of how to create mobile-friendly animations with SVG in Flutter. Start experimenting and incorporate SVG animations into your Flutter projects to create stunning user experiences.

# References

- Flutter documentation: https://flutter.dev/docs
- SVG website: https://www.w3schools.com/svg/
- `flutter_svg` package documentation: https://pub.dev/packages/flutter_svg
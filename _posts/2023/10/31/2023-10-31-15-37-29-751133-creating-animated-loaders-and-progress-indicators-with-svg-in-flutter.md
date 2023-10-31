---
layout: post
title: "Creating animated loaders and progress indicators with SVG in Flutter"
description: " "
date: 2023-10-31
tags: [references]
comments: true
share: true
---

In today's world of fast-paced development, creating visually appealing and responsive loaders and progress indicators is crucial in providing a smooth user experience. Flutter, a popular cross-platform framework, allows developers to easily create custom loaders and progress indicators using Scalable Vector Graphics (SVG).

SVG files are XML-based vector images that can be easily manipulated, styled, and animated. By leveraging the power of SVG, developers can create highly customizable and visually stunning loaders and progress indicators in Flutter.

## Getting Started

To get started, you need to import the flutter_svg package in your Flutter project. Open your `pubspec.yaml` file and add the following line to your dependencies:

```dart
dependencies:
  flutter_svg: any
```

Run `flutter pub get` to fetch the package.

## Using SVG in Flutter

Once you have the flutter_svg package installed, you can start using SVG files in your Flutter app. Place your SVG files in the `assets` folder of your project.

To display an SVG image, you can use the `SvgPicture.asset` widget. Here's an example:

```dart
import 'package:flutter_svg/flutter_svg.dart';

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return SvgPicture.asset('assets/loader.svg');
  }
}
```

This code snippet will display the `loader.svg` image located in the `assets` directory.

## Animating SVG Images

To create animated loaders and progress indicators, you can use the `flutter_svg` package's built-in animation capabilities. Flutter provides several ways to animate SVG images, such as using the `AnimatedContainer` widget or the `AnimationController`.

Here's an example of using the `AnimationController` to animate an SVG loader:

```dart
import 'package:flutter_svg/flutter_svg.dart';

class MyLoader extends StatefulWidget {
  @override
  _MyLoaderState createState() => _MyLoaderState();
}

class _MyLoaderState extends State<MyLoader>
    with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 2),
      vsync: this,
    )..repeat(reverse: true);
    _animation = Tween<double>(
      begin: 0.0,
      end: 1.0,
    ).animate(_controller);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _animation,
      builder: (BuildContext context, Widget? child) {
        return Transform.rotate(
          angle: _animation.value * 2 * pi,
          child: SvgPicture.asset('assets/loader.svg'),
        );
      },
    );
  }
}
```

In this example, we use an `AnimationController` to animate the rotation of the SVG loader image. The `AnimatedBuilder` widget rebuilds the UI whenever the animation value changes, allowing us to update the rotation angle based on the animation progress.

## Customization

One of the major advantages of using SVG files in Flutter is the ability to customize and style them easily. You can modify SVG properties like color, size, stroke, or fill to match the design of your app or brand.

To change the color of an SVG image, you can use the `color` property of the `SvgPicture.asset` widget. For example:

```dart
SvgPicture.asset(
  'assets/loader.svg',
  color: Colors.blue,
),
```

This code snippet will display the `loader.svg` image with a blue color.

## Conclusion

By leveraging SVG files and the `flutter_svg` package, Flutter developers can create highly customizable and visually appealing loaders and progress indicators. With the ability to animate SVG images and easily customize their appearance, developers can provide a seamless user experience that improves the overall quality of their Flutter apps.

Start exploring SVG loaders and progress indicators in Flutter today and enhance your app's user interface!

#references
- [Flutter documentation](https://flutter.dev/)
- [Flutter SVG package](https://pub.dev/packages/flutter_svg)
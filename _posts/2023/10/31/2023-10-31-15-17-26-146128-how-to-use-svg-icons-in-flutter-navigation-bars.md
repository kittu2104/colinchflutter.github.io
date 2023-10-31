---
layout: post
title: "How to use SVG icons in Flutter navigation bars"
description: " "
date: 2023-10-31
tags: []
comments: true
share: true
---

In Flutter, navigation bars are an essential part of many mobile applications. They help users navigate through different screens or sections of the app. One way to enhance the visual appeal of navigation bars is by using SVG icons. Scalable Vector Graphics (SVG) icons provide high-quality and resolution-independent graphics, ensuring that your navigation bar looks great on any screen size.

In this tutorial, we will explore how to use SVG icons in Flutter navigation bars.

## Prerequisites
Before we begin, make sure you have the following:
- Flutter SDK installed on your machine
- A Flutter project set up

## Steps

### 1. Add the `flutter_svg` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_svg: ^0.22.0
```

### 2. Run `flutter pub get` command to fetch the package.

### 3. Import the necessary packages in your Dart file:

```dart
import 'package:flutter_svg/flutter_svg.dart';
```

### 4. Copy your SVG icon file to the project's `assets` folder.

### 5. Update the `pubspec.yaml` file to include the path to your SVG file:

```yaml
flutter:
  assets:
  - assets/icon.svg
```

### 6. Use the `SvgPicture.asset` widget to display the SVG icon in your navigation bar:

```dart
BottomNavigationBarItem(
  icon: SvgPicture.asset(
    'assets/icon.svg',
    width: 24,
    height: 24,
  ),
  label: 'Home',
),
```

Make sure to adjust the `width` and `height` values according to your design requirements.

### 7. Repeat step 6 for the other navigation items you want to display.

## Conclusion

By using SVG icons in your Flutter navigation bars, you can enhance the visual appeal and create resolution-independent graphics. The `flutter_svg` package makes it easy to integrate SVG icons into your application.

Give it a try, and let your navigation bar shine with beautiful and scalable icons!

#References
- Flutter SVG package: [https://pub.dev/packages/flutter_svg](https://pub.dev/packages/flutter_svg)
- Flutter documentation: [https://flutter.dev/docs](https://flutter.dev/docs)
---
layout: post
title: "Creating custom icons using SVG in Flutter"
description: " "
date: 2023-10-31
tags: [icons]
comments: true
share: true
---

In Flutter, we often need to use custom icons in our applications to give them a unique look and feel. While Flutter provides a vast collection of pre-built icons, sometimes we might need to create and use our own custom icons.

One popular approach to creating custom icons in Flutter is by using SVG (Scalable Vector Graphics) files. SVG files are lightweight and scalable, making them a great choice for creating icons with smooth edges and consistent proportions.

Here are the steps to create and use custom icons using SVG in Flutter:

## Step 1: Get the SVG file
You can use any vector editing software, such as Adobe Illustrator or Inkscape, to create your custom icon as an SVG file. Alternatively, you can also find SVG resources online or convert existing vector image files to SVG format.

## Step 2: Add `flutter_svg` dependency
In your Flutter project, open the `pubspec.yaml` file and add the following dependency to use the `flutter_svg` package:

```yaml
dependencies:
  flutter_svg: ^0.22.0
```

Save the file and run the `flutter pub get` command in your terminal or IDE to fetch the package.

## Step 3: Place the SVG file in your project
Create a folder in your project directory, such as `assets/icons`, and place the SVG file inside it. Make sure to mention the SVG file path in the `pubspec.yaml` file under the `flutter` section:

```yaml
flutter:
  assets:
    - assets/icons/
```

Save the file and run the `flutter pub get` command again to include the SVG file in your project.

## Step 4: Use the SVG icon in your code
In your Dart code, import the `flutter_svg` package:

```dart
import 'package:flutter_svg/flutter_svg.dart';
```

To use the custom SVG icon, you can use the `SvgPicture.asset` widget like this:

```dart
SvgPicture.asset(
  'assets/icons/my_custom_icon.svg',
  width: 24, // specify the desired size
  height: 24,
)
```

Make sure to provide the correct path to your SVG file. You can also adjust the width and height according to your requirements.

That's it! You have successfully created and used a custom icon using SVG in Flutter. You can now customize the appearance and behavior of your icon just like any other Flutter widget.

## Conclusion
Creating custom icons using SVG in Flutter allows us to have full control over the design and customization of our application. With the help of the `flutter_svg` package, integrating SVG icons into our Flutter project becomes a seamless process.

Give it a try and have fun creating your own custom icons! Happy coding!

## References
- [Flutter SVG package documentation](https://pub.dev/packages/flutter_svg)
- [SVG on MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/SVG)
- [Flutter documentation](https://flutter.dev/docs) 

#flutter #icons
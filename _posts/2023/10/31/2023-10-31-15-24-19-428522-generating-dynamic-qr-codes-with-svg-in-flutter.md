---
layout: post
title: "Generating dynamic QR codes with SVG in Flutter"
description: " "
date: 2023-10-31
tags: []
comments: true
share: true
---

In this blog post, we will explore how to generate dynamic QR codes using Scalable Vector Graphics (SVG) in the Flutter framework. QR codes have become increasingly popular for sharing information such as URLs, contact details, or product information. By integrating SVG in Flutter, we can generate and display QR codes that are not pixelated and can be easily resized without losing their quality.

## What is SVG?

SVG is an XML-based vector image format widely used for rendering graphics on the web. Unlike raster-based image formats like JPEG or PNG, SVG images are resolution-independent. This means that they can be scaled up or down without the loss of quality.

## Generating QR codes in Flutter

Flutter provides several packages that allow us to generate QR codes. One popular package is `qr_flutter`, which simplifies the process of generating and displaying QR codes.

To get started, add the `qr_flutter` package to your Flutter project by adding it as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  qr_flutter: ^4.0.0
```

Next, import the necessary packages in your widget file:

```dart
import 'package:flutter/material.dart';
import 'package:qr_flutter/qr_flutter.dart';
```

Now, you can generate a QR code by providing the desired data and customization options. For example, to generate a QR code with the text "Hello, World!" and a size of 200 pixels, you can use the following code:

```dart
QrImage(
  data: 'Hello, World!',
  size: 200.0,
)
```

This will display the QR code as an image in your Flutter app.

## Using SVG instead of bitmap images

To generate a QR code as an SVG image instead of a bitmap image, we can make use of the `svg` package in Flutter. This package allows us to programmatically generate SVG images.

First, add the `flutter_svg` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_svg: ^1.0.0
```

Import the package in your widget file:

```dart
import 'package:flutter_svg/flutter_svg.dart';
```

Instead of using the `QrImage` widget, we can now use the `SvgPicture.string` constructor to convert the SVG XML string into a `Widget`. Here's an example:

```dart
SvgPicture.string(
  qrCodeSvgString,
  width: 200.0,
  height: 200.0,
)
```

In the above code, `qrCodeSvgString` is the SVG XML string representation of the QR code generated using the `qr_flutter` package.

## Conclusion

In this blog post, we explored how to generate dynamic QR codes using SVG in Flutter. By leveraging the `qr_flutter` package for QR code generation and the `flutter_svg` package for rendering SVG images, we can generate high-quality QR codes that are resolution-independent and easily resizable.

With this knowledge, you can now create custom QR code generators in your Flutter apps and enhance the user experience by displaying QR codes with precise dimensions and clear components. Happy coding!

# References
- [qr_flutter package on pub.dev](https://pub.dev/packages/qr_flutter)
- [flutter_svg package on pub.dev](https://pub.dev/packages/flutter_svg)
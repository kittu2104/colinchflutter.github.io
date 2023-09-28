---
layout: post
title: "Using CustomClipper to create a custom QR code shape in Flutter"
description: " "
date: 2023-09-21
tags: [qrcode, customshape]
comments: true
share: true
---

QR codes are a popular way to encode information, such as URLs, contact information, or text. In Flutter, we can use the `qr_flutter` package to generate QR codes. However, sometimes we may want to give the QR code a custom shape to better match our app's design.

In this article, we will explore how to use the `CustomClipper` class in Flutter to create a custom shape for our QR codes.

## Prerequisites

Before we begin, make sure you have Flutter SDK installed on your machine. You can follow the [official Flutter installation guide](https://flutter.dev/docs/get-started/install) to get started.

## Creating the Flutter Project

Let's start by creating a new Flutter project. Open your terminal or command prompt and run the following command:

```shell
flutter create custom_qr_code
```

After the project is created successfully, navigate to the project folder using the `cd` command:

```shell
cd custom_qr_code
```

## Adding the Dependencies

Next, we need to add the `qr_flutter` package to our project. Open the `pubspec.yaml` file in your project and add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter:
    sdk: flutter
  qr_flutter: ^3.0.0
```

Save the file and run the following command to install the package:

```shell
flutter pub get
```

## Creating a Custom QR Code Shape

To create a custom QR code shape, we will define a custom `CustomClipper` class and override the `getClip` method. This method will be responsible for returning the custom shape as a `Path` object.

Here's an example of a custom QR code shape that resembles a circular frame:

```dart
import 'package:flutter/material.dart';

class CircularFrameClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    final path = Path();
    path.addRRect(RRect.fromRectAndRadius(
      Rect.fromLTWH(0, 0, size.width, size.height),
      Radius.circular(size.width / 2),
    ));
    path.addOval(Rect.fromCircle(
      center: Offset(size.width / 2, size.height / 2),
      radius: size.width / 4,
    ));
    path.fillType = PathFillType.evenOdd;
    return path;
  }

  @override
  bool shouldReclip(CircularFrameClipper oldClipper) => false;
}
```

In the above code, we define a `CircularFrameClipper` class that extends the `CustomClipper<Path>` class. Inside the `getClip` method, we create a `Path` object and add a rounded rectangle shape covering the entire size of the widget. Then, we add an oval shape in the center of the widget to create the circular frame. Finally, we set the `fillType` to `PathFillType.evenOdd`, which allows us to create a hollow shape.

## Using the Custom QR Code Shape

Now that we have defined our custom QR code shape, let's use it in a Flutter widget. In the `lib/main.dart` file, replace the existing `MyApp` class with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:qr_flutter/qr_flutter.dart';

import 'circular_frame_clipper.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom QR Code',
      home: Scaffold(
        appBar: AppBar(title: Text('Custom QR Code')),
        body: Center(
          child: ClipPath(
            clipper: CircularFrameClipper(),
            child: Container(
              width: 200,
              height: 200,
              color: Colors.white,
              child: QrImage(
                data: 'https://example.com',
                version: QrVersions.auto,
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

In the above code, we import our custom `CircularFrameClipper` class and use it as the `clipper` property of the `ClipPath` widget. Inside the `Container`, we set its dimensions and background color, and then use the `QrImage` widget from the `qr_flutter` package to generate the QR code. The resulting QR code will conform to our custom circular frame shape.

## Running the App

To run the app, execute the following command in your terminal:

```shell
flutter run
```

You should see the custom QR code shape with the circular frame in the center. Feel free to further customize the `CircularFrameClipper` class to match your desired shape and design.

That's it! In this article, we learned how to use the `CustomClipper` class in Flutter to create a custom shape for QR codes. By defining our own `CustomClipper` class and using it in conjunction with the `qr_flutter` package, we can easily create unique QR codes that match our app's design requirements.

#flutter #qrcode #customshape
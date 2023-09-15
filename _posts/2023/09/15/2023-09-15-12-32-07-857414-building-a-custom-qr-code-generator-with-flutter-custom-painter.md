---
layout: post
title: "Building a custom QR code generator with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [flutter, qrcode]
comments: true
share: true
---

In this tutorial, we will explore how to build a custom QR code generator using Flutter's Custom Painter. QR codes have become increasingly popular for encoding information such as URLs, contact details, and more. The ability to generate QR codes dynamically in our Flutter application can add versatility and functionality to our projects.

### Getting Started

To begin, make sure you have Flutter installed and set up on your machine. If you haven't already, you can follow the official Flutter installation guide: [https://flutter.dev/docs/get-started/install](https://flutter.dev/docs/get-started/install)

### Project Setup

Create a new Flutter project by running the following command in your terminal:

```bash
flutter create custom_qr_code_generator
cd custom_qr_code_generator
```

### Installing Dependencies

Open the `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  qr_flutter: ^5.1.0
```

Save the file and run the following command to install the dependencies:

```bash
flutter pub get
```

### Generating QR Codes

First, we need to import the necessary packages for generating QR codes and the Custom Painter. Add the following import statements at the top of the `main.dart` file:

```dart
import 'package:flutter/material.dart';
import 'package:qr_flutter/qr_flutter.dart';
```

![Custom QR Code Generator](assets/qrcode_example.png)

Next, define a new class called `QRCodeGenerator` that extends the `CustomPainter` class. This class will handle the actual generation and drawing of the QR code.

```dart
class QRCodeGenerator extends CustomPainter {
  final String data;
  final Color color;
  final Color backgroundColor;

  QRCodeGenerator({required this.data, required this.color, required this.backgroundColor});

  @override
  void paint(Canvas canvas, Size size) {
    final qrCode = QrCode.fromData(data: data);

    final paint = Paint()
      ..color = backgroundColor
      ..style = PaintingStyle.fill;

    canvas.drawRect(Rect.fromLTWH(0, 0, size.width, size.height), paint);

    final cellSize = size.width / qrCode.width;

    for (var x = 0; x < qrCode.width; x++) {
      for (var y = 0; y < qrCode.width; y++) {
        final offset = Offset(x.toDouble() * cellSize, y.toDouble() * cellSize);
        final color = qrCode.isDark(y, x) ? this.color : backgroundColor;
        final cellRect = Rect.fromLTWH(offset.dx, offset.dy, cellSize, cellSize);

        paint.color = color;
        canvas.drawRect(cellRect, paint);
      }
    }
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}
```

This code defines a class `QRCodeGenerator` that takes in the `data` (the information to encode in the QR code), the `color` (dark color of the QR code cells), and the `backgroundColor` (light color of the QR code background). The `paint` method is where the QR code is generated and drawn using the QRFlutter package.

### Implementing the QR Code Widget

In the `main.dart` file, replace the default `MyApp` class with the following code:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom QR Code Generator',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Custom QR Code Generator'),
        ),
        body: Center(
          child: Container(
            width: 200,
            height: 200,
            child: CustomPaint(
              painter: QRCodeGenerator(
                data: 'https://example.com',
                color: Colors.black,
                backgroundColor: Colors.white,
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

In this code, we define a `Center` widget that contains a `Container` with fixed dimensions. Inside the `Container`, we use the `CustomPaint` widget to paint our custom QR code using the `QRCodeGenerator` class we created earlier. You can customize the data, color, and background color accordingly.

### Running the Application

Finally, run the application using the following command:

```bash
flutter run
```

This will launch the app on a connected device or emulator, and you should see a QR code displayed in the middle of the screen. You can customize the QR code data, color, and background color to suit your needs.

### Conclusion

In this tutorial, we learned how to build a custom QR code generator using Flutter's Custom Painter. We explored how to generate and draw a QR code using the qr_flutter package, and we implemented a custom painter to handle the drawing. With this knowledge, you can now easily incorporate QR code generation into your Flutter applications. Enjoy experimenting and building amazing applications with QR codes!

#flutter #qrcode #custompainter
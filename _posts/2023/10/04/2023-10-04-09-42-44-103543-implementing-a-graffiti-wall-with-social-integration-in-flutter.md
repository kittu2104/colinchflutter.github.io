---
layout: post
title: "Implementing a graffiti wall with social integration in Flutter"
description: " "
date: 2023-10-04
tags: [setting, creating]
comments: true
share: true
---

Flutter, Google's UI toolkit for building natively compiled applications for mobile, web, and desktop provides a rich set of features and functionalities. In this tutorial, we will explore how to implement a graffiti wall with social integration using Flutter.

## Table of Contents
1. [Setting up the project](#setting-up-the-project)
2. [Creating the graffiti wall](#creating-the-graffiti-wall)
3. [Integrating social features](#integrating-social-features)
4. [Conclusion](#conclusion)

## Setting up the project

To begin, make sure you have Flutter properly installed and set up on your system. You can refer to the official Flutter documentation for installation instructions.

Once Flutter is set up, create a new Flutter project using the following command:

```dart
flutter create graffiti_wall
```

Change to the project directory:

```dart
cd graffiti_wall
```

Open `lib/main.dart` and remove the existing code. Replace it with the following code to set up a basic Flutter app structure:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(GraffitiWallApp());
}

class GraffitiWallApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Graffiti Wall',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: GraffitiWallScreen(),
    );
  }
}

class GraffitiWallScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Graffiti Wall'),
      ),
      body: Center(
        child: Text(
          'Welcome to the Graffiti Wall',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

Save the file and run the app using the following command:

```dart
flutter run
```

You should now see the basic Graffiti Wall app running on your device or emulator.

## Creating the graffiti wall

To implement the graffiti wall functionality, we will use a `Canvas` widget provided by Flutter. The `Canvas` widget allows us to draw on the screen using low-level graphics primitives.

Open `lib/main.dart` and replace the `GraffitiWallScreen` class with the following code:

```dart
class GraffitiWallScreen extends StatefulWidget {
  @override
  _GraffitiWallScreenState createState() => _GraffitiWallScreenState();
}

class _GraffitiWallScreenState extends State<GraffitiWallScreen> {
  List<Offset> _points = [];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Graffiti Wall'),
      ),
      body: GestureDetector(
        onPanUpdate: (DragUpdateDetails details) {
          setState(() {
            RenderBox renderBox = context.findRenderObject();
            Offset localPosition = renderBox.globalToLocal(details.globalPosition);
            _points = List.from(_points)..add(localPosition);
          });
        },
        onPanEnd: (DragEndDetails details) => _points.add(null),
        child: CustomPaint(
          painter: GraffitiPainter(_points),
        ),
      ),
    );
  }
}

class GraffitiPainter extends CustomPainter {
  final List<Offset> points;

  GraffitiPainter(this.points);

  @override
  void paint(Canvas canvas, Size size) {
    Paint paint = Paint()
      ..color = Colors.black
      ..strokeCap = StrokeCap.round
      ..strokeWidth = 5.0;

    for (int i = 0; i < points.length - 1; i++) {
      if (points[i] != null && points[i + 1] != null) {
        canvas.drawLine(points[i], points[i + 1], paint);
      }
    }
  }

  @override
  bool shouldRepaint(GraffitiPainter oldDelegate) => true;
}
```

This code sets up a `GraffitiWallScreen` widget as a stateful widget. It uses a `GestureDetector` widget to detect user interactions on the screen, and a `CustomPaint` widget to draw on the canvas.

Save the file and run the app again. Now, you should be able to draw on the screen by dragging your finger or cursor.

## Integrating social features

To add social integration to our graffiti wall, we can leverage Flutter's existing packages that provide social media sharing functionality. For example, we can use the `share` package to allow users to share their graffiti wall creations.

To integrate the `share` package, open `pubspec.yaml` and add the following dependency:

```dart
dependencies:
  flutter:
    sdk: flutter

  share: ^2.0.1
```

Save the file and run the following command to install the dependencies:

```dart
flutter pub get
```

Now, open `lib/main.dart` and update the `GraffitiWallScreen` class with the following code:

```dart
import 'package:share/share.dart';

// ...

class _GraffitiWallScreenState extends State<GraffitiWallScreen> {
  // ...

  Future<void> _shareGraffiti() async {
    final recorder = ui.PictureRecorder();
    final canvas = Canvas(recorder);

    final painter = GraffitiPainter(_points);
    painter.paint(canvas, Size.infinite);

    final picture = recorder.endRecording();
    final image = await picture.toImage(size.width.toInt(), size.height.toInt());
    final byteData = await image.toByteData(format: ui.ImageByteFormat.png);
    final tempPath = await getTemporaryDirectory();
    final filePath = "${tempPath.path}/graffiti_wall.png";
    final file = File(filePath);
    await file.writeAsBytes(byteData.buffer.asUint8List());

    Share.shareFiles([filePath], text: 'Check out my graffiti creation!');
  }

  // ...

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Graffiti Wall'),
        actions: <Widget>[
          IconButton(
            icon: Icon(Icons.share),
            onPressed: _shareGraffiti,
          ),
        ],
      ),
      // ...
    );
  }
}
```

This code adds a share button to the app's `AppBar` and defines a `_shareGraffiti` method that captures the current graffiti art, saves it as an image, and shares it using the `share` package.

Save the file and run the app again. You can now draw on the graffiti wall and share your creations using the share button in the app's header.

## Conclusion

In this tutorial, we explored how to implement a graffiti wall with social integration using Flutter. We learned about using the `Canvas` widget to draw on the screen and integrating the `share` package to enable social media sharing functionality. Feel free to enhance the app by adding additional features like color selection or saving graffiti creations locally.

#flutter #graffiti #social #integration
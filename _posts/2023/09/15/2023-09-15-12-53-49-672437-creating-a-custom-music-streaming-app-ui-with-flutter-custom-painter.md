---
layout: post
title: "Creating a custom music streaming app UI with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [flutter, custompainter]
comments: true
share: true
---

Flutter offers a robust set of UI widgets that allow developers to build beautiful and responsive apps. In addition to the built-in widgets, Flutter also provides a powerful tool called **CustomPainter** that allows developers to create custom UI elements with complete control over how they are drawn.

In this tutorial, we will walk through the process of creating a custom music streaming app UI using Flutter CustomPainter. We will design a simple music player interface with play, pause, and skip buttons, as well as a progress bar.

## Setting up the Project

First, let's set up a new Flutter project by running the following command in your terminal:

```plaintext
$ flutter create custom_music_player
```

Navigate to the project directory:

```plaintext
$ cd custom_music_player
```

Now, open the project in your favorite code editor.

## Creating the CustomPainter

Create a new file called `music_player_painter.dart`. This file will house our custom painter implementation. Add the following code to define our custom painter class:

```dart
import 'package:flutter/material.dart';

class MusicPlayerPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Implement custom painting logic here
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false; // Returning false since we won't be repainting
  }
}
```

## Designing the Music Player UI

Let's start by designing the UI for our music player. Open the `lib/main.dart` file and replace the default template code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MusicPlayerApp());
}

class MusicPlayerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        appBar: AppBar(
          title: Text('Music Player'),
        ),
        body: Container(
          child: Center(
            child: CustomPaint(
              painter: MusicPlayerPainter(),
            ),
          ),
        ),
      ),
    );
  }
}
```

## Customizing the Music Player UI

Inside the `MusicPlayerPainter` class, we will implement our custom painting logic. For example, we can draw the play, pause, and skip buttons, as well as the progress bar.

```dart
@override
void paint(Canvas canvas, Size size) {
  final paint = Paint()
    ..color = Colors.grey
    ..style = PaintingStyle.fill;

  final buttonRadius = 20.0;
  final spacing = 20.0;
  
  // Draw play button
  canvas.drawCircle(
    Offset(size.width / 2 - buttonRadius - spacing, size.height / 2),
    buttonRadius,
    paint,
  );

  // Draw pause button
  canvas.drawRect(
    Rect.fromLTWH(
      size.width / 2 - buttonRadius,
      size.height / 2 - buttonRadius,
      buttonRadius,
      buttonRadius * 2,
    ),
    paint,
  );

  // Draw skip button
  canvas.drawCircle(
    Offset(size.width / 2 + buttonRadius + spacing, size.height / 2),
    buttonRadius,
    paint,
  );

  // Draw progress bar
  final progressBarWidth = size.width * 0.7;
  final progressBarHeight = 5.0;
  final progressFill = Paint()
    ..color = Colors.blue
    ..style = PaintingStyle.fill;

  canvas.drawRect(
    Rect.fromLTWH(
      size.width / 2 - progressBarWidth / 2,
      size.height * 0.75 - progressBarHeight / 2,
      progressBarWidth,
      progressBarHeight,
    ),
    paint,
  );

  // Draw progress fill
  canvas.drawRect(
    Rect.fromLTWH(
      size.width / 2 - progressBarWidth / 2,
      size.height * 0.75 - progressBarHeight / 2,
      progressBarWidth * 0.5,
      progressBarHeight,
    ),
    progressFill,
  );
}
```

## Running the App

Save the changes and run the app using the following command:

```plaintext
$ flutter run
```

You should now see the music player interface with the custom buttons and progress bar. Feel free to customize the UI further according to your requirements.

## Conclusion

In this tutorial, we learned how to create a custom music streaming app UI using Flutter CustomPainter. We utilized the power of Flutter's CustomPainter class to draw custom UI elements such as buttons and progress bars. Custom painters provide complete control over the appearance and behavior of UI components, enabling developers to create unique and visually appealing interfaces.

#flutter #custompainter
---
layout: post
title: "Implementing a custom countdown timer with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [CustomPainter]
comments: true
share: true
---

In this tutorial, we will explore how to create a custom countdown timer using Flutter's CustomPainter class. Flutter's CustomPainter provides a powerful way to generate custom graphics and animations. We will utilize this to create a countdown timer widget with a visually appealing design.

## Setting up the Project

Before we begin, ensure that you have Flutter installed and set up on your machine. Create a new Flutter project and open it in your preferred code editor.

## Creating the CountdownTimer Widget

First, we'll create a new Dart file called `countdown_timer.dart`. This file will contain our custom countdown timer widget.

```dart
import 'dart:async';
import 'package:flutter/material.dart';

class CountdownTimer extends StatefulWidget {
  final int seconds;
  final Color backgroundColor;
  final Color circleColor;
  final Color countdownColor;

  CountdownTimer({
    required this.seconds,
    this.backgroundColor = Colors.white,
    this.circleColor = Colors.blue,
    this.countdownColor = Colors.red,
  });

  @override
  _CountdownTimerState createState() => _CountdownTimerState();
}

class _CountdownTimerState extends State<CountdownTimer> {
  late Timer _timer;
  int _currentSeconds = 0;

  @override
  void initState() {
    super.initState();
    _currentSeconds = widget.seconds;
    _startTimer();
  }

  @override
  void dispose() {
    _timer.cancel();
    super.dispose();
  }

  void _startTimer() {
    const oneSec = Duration(seconds: 1);
    _timer = Timer.periodic(oneSec, (timer) {
      if (_currentSeconds == 0) {
        timer.cancel();
      } else {
        setState(() {
          _currentSeconds--;
        });
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: widget.backgroundColor,
      body: Center(
        child: CustomPaint(
          painter: TimerPainter(
            circleColor: widget.circleColor,
            countdownColor: widget.countdownColor,
            currentProgress: (_currentSeconds / widget.seconds),
          ),
          child: Container(
            width: 200,
            height: 200,
            child: Center(
              child: Text(
                '$_currentSeconds',
                style: TextStyle(fontSize: 48, fontWeight: FontWeight.bold),
              ),
            ),
          ),
        ),
      ),
    );
  }
}

class TimerPainter extends CustomPainter {
  final Color circleColor;
  final Color countdownColor;
  final double currentProgress;

  TimerPainter({
    required this.circleColor,
    required this.countdownColor,
    required this.currentProgress,
  });

  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()
      ..color = circleColor
      ..strokeWidth = 12
      ..strokeCap = StrokeCap.round
      ..style = PaintingStyle.stroke;

    final countDownPaint = Paint()
      ..color = countdownColor
      ..strokeWidth = 12
      ..strokeCap = StrokeCap.round
      ..style = PaintingStyle.stroke;

    final offsetCenter = Offset(size.width / 2, size.height / 2);
    final radius = (size.width - paint.strokeWidth) / 2;

    canvas.drawCircle(offsetCenter, radius, paint);

    final progressAngle = 2 * 3.1416 * (1 - currentProgress);

    canvas.drawArc(
      Rect.fromCircle(center: offsetCenter, radius: radius),
      0,
      progressAngle,
      false,
      countDownPaint,
    );
  }

  @override
  bool shouldRepaint(TimerPainter oldDelegate) {
    return oldDelegate.currentProgress != currentProgress;
  }
}
```

## Using the CountdownTimer Widget

To use the CountdownTimer widget, simply add it to your desired Flutter screen or widget tree.

```dart
import 'package:flutter/material.dart';
import 'package:your_project_name/countdown_timer.dart';

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Countdown Timer'),
      ),
      body: Center(
        child: CountdownTimer(
          seconds: 60,
          backgroundColor: Colors.white,
          circleColor: Colors.blue,
          countdownColor: Colors.red,
        ),
      ),
    );
  }
}
```

## Conclusion

In this tutorial, we learned how to implement a custom countdown timer using Flutter's CustomPainter class. We created a reusable CountdownTimer widget and utilized the CustomPainter class to draw and animate the countdown timer. By customizing the widget properties, you can experiment with different colors and styles to match your app's design.

#Flutter #CustomPainter #CountdownTimer
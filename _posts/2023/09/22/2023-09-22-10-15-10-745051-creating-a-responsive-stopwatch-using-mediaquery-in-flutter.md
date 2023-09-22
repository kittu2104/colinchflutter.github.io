---
layout: post
title: "Creating a responsive stopwatch using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [Flutter, Stopwatch]
comments: true
share: true
---

Stopwatches are handy tools that allow you to measure the elapsed time accurately. In this tutorial, we will explore how to create a responsive stopwatch using `MediaQuery` in Flutter.

## Getting Started

To begin, create a new Flutter project and open it in your preferred code editor. Replace the code in the `lib/main.dart` file with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Stopwatch',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: StopWatchPage(),
    );
  }
}

class StopWatchPage extends StatefulWidget {
  @override
  _StopWatchPageState createState() => _StopWatchPageState();
}

class _StopWatchPageState extends State<StopWatchPage> {
  double stopwatchHeight;

  @override
  Widget build(BuildContext context) {
    stopwatchHeight = MediaQuery.of(context).size.height * 0.6;

    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Stopwatch'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Container(
              height: stopwatchHeight,
              width: stopwatchHeight,
              decoration: BoxDecoration(
                color: Colors.grey[300],
                shape: BoxShape.circle,
              ),
              child: Center(
                child: Text(
                  '00:00:00',
                  style: TextStyle(fontSize: 48),
                ),
              ),
            ),
            SizedBox(height: 24),
            Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                RaisedButton(
                  onPressed: () {},
                  child: Text('Start'),
                ),
                SizedBox(width: 12),
                RaisedButton(
                  onPressed: () {},
                  child: Text('Stop'),
                ),
                SizedBox(width: 12),
                RaisedButton(
                  onPressed: () {},
                  child: Text('Reset'),
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
```

In the above code, we have created a basic Flutter application with a responsive stopwatch widget. The stopwatch's height will adjust according to the device's screen height using the `MediaQuery` class.

The `StopWatchPage` widget is a StatefulWidget that holds the state for the stopwatch. Inside the `build` method, we calculate the desired height for the stopwatch using `MediaQuery.of(context).size.height` and assign it to the `stopwatchHeight` variable.

Inside the `Scaffold` widget's `body`, we create a column layout with a `Container` widget as the stopwatch holder. The height and width of the container are set to `stopwatchHeight`, and we apply a circular shape using the `BoxDecoration`. The stopwatch's time is displayed using a `Text` widget inside the container.

Below the stopwatch, we have placed three `RaisedButton` widgets for the start, stop, and reset functionalities.

Congratulations! You have successfully created a responsive stopwatch using `MediaQuery` in Flutter.

Stay tuned for more Flutter tutorials and happy coding!

## #Flutter #Stopwatch
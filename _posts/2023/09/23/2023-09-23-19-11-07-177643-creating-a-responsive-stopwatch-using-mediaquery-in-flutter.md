---
layout: post
title: "Creating a responsive stopwatch using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [Stopwatch]
comments: true
share: true
---

Stopwatches are essential tools in various applications. In this tutorial, we will learn how to create a responsive stopwatch using `MediaQuery` in Flutter. `MediaQuery` allows us to adapt our UI based on the device's screen size and orientation, ensuring our stopwatch looks and functions well across different devices.

## Prerequisites

To follow along with this tutorial, make sure you have Flutter installed and set up on your machine.

## Steps

### Step 1: Create a new Flutter project

Create a new Flutter project by running the following command in your terminal:

```dart
flutter create responsive_stopwatch
```

### Step 2: Modify the `pubspec.yaml` file

In the `pubspec.yaml` file, add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
```

After adding the dependencies, run `flutter pub get` to fetch and install the added dependencies.

### Step 3: Create the Stopwatch widget

Open the `lib/main.dart` file and replace its content with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive Stopwatch'),
        ),
        body: StopwatchWidget(),
      ),
    );
  }
}

class StopwatchWidget extends StatefulWidget {
  @override
  _StopwatchWidgetState createState() => _StopwatchWidgetState();
}

class _StopwatchWidgetState extends State<StopwatchWidget> {
  Duration _duration = Duration();
  bool _isRunning = false;

  void _startStopwatch() {
    if (_isRunning) {
      return;
    }
    setState(() {
      _isRunning = true;
    });
    _updateStopwatch();
  }

  void _updateStopwatch() {
    WidgetsBinding.instance.addPostFrameCallback((_) {
      if (_isRunning) {
        setState(() {
          _duration = _duration + Duration(milliseconds: 10);
        });
        _updateStopwatch();
      }
    });
  }

  void _stopStopwatch() {
    if (!_isRunning) {
      return;
    }
    setState(() {
      _isRunning = false;
    });
  }

  void _resetStopwatch() {
    setState(() {
      _duration = Duration();
    });
  }

  String _formatMilliseconds(int milliseconds) {
    int minutes = milliseconds ~/ 60000;
    int seconds = (milliseconds ~/ 1000) % 60;
    int milliSeconds = (milliseconds % 1000) ~/ 10;

    String formattedTime =
        '${minutes.toString().padLeft(2, '0')}:'
        '${seconds.toString().padLeft(2, '0')}.'
        '${milliSeconds.toString().padLeft(2, '0')}';

    return formattedTime;
  }

  @override
  Widget build(BuildContext context) {
    final screenWidth = MediaQuery.of(context).size.width;
    final screenHeight = MediaQuery.of(context).size.height;

    final stopwatchTextSize = screenHeight * 0.1;
    final buttonFontSize = screenHeight * 0.03;

    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Text(
          _formatMilliseconds(_duration.inMilliseconds),
          style: TextStyle(
            fontSize: stopwatchTextSize,
            fontWeight: FontWeight.bold,
          ),
        ),
        SizedBox(height: screenHeight * 0.05),
        Row(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            RaisedButton(
              onPressed: _isRunning ? _stopStopwatch : _startStopwatch,
              child: Text(
                _isRunning ? 'Stop' : 'Start',
                style: TextStyle(
                  fontSize: buttonFontSize,
                  fontWeight: FontWeight.bold,
                ),
              ),
            ),
            SizedBox(width: screenWidth * 0.05),
            RaisedButton(
              onPressed: _resetStopwatch,
              child: Text(
                'Reset',
                style: TextStyle(
                  fontSize: buttonFontSize,
                  fontWeight: FontWeight.bold,
                ),
              ),
            ),
          ],
        ),
      ],
    );
  }
}
```

### Step 4: Run the app

Save the changes and run the app using the following command:

```dart
flutter run
```

You should now see the responsive stopwatch app running on your simulator or device.

## Conclusion

In this tutorial, we learned how to create a responsive stopwatch using `MediaQuery` in Flutter. By adapting the UI based on the device's screen size, our stopwatch remains visually appealing and functional across different devices. Happy coding!

#Flutter #Stopwatch
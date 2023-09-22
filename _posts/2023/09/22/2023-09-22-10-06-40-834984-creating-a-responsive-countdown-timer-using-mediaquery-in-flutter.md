---
layout: post
title: "Creating a responsive countdown timer using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [flutter, responsive]
comments: true
share: true
---

In Flutter, `MediaQuery` is a powerful tool that allows us to make our app responsive to different screen sizes and orientations. In this tutorial, we will learn how to create a responsive countdown timer by utilizing `MediaQuery`.

## Step 1: Set up a new Flutter project

First, make sure you have Flutter installed on your machine. Then, create a new Flutter project by running the following command in your terminal:

```dart
flutter create countdown_timer_app
```

## Step 2: Define the Countdown Timer Widget

In the `lib` folder of your Flutter project, open the `main.dart` file. Inside the `main()` function, replace the default code with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(CountdownTimerApp());
}

class CountdownTimerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Countdown Timer App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: CountdownTimerPage(),
    );
  }
}

class CountdownTimerPage extends StatefulWidget {
  @override
  _CountdownTimerPageState createState() => _CountdownTimerPageState();
}

class _CountdownTimerPageState extends State<CountdownTimerPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Countdown Timer'),
      ),
      body: Center(
        child: Text('Countdown Timer'),
      ),
    );
  }
}
```

## Step 3: Add a Countdown Timer

Now we can add a `CountdownTimer` widget to the `_CountdownTimerPageState` class. Update the `_CountdownTimerPageState` class as follows:

```dart
import 'package:flutter/material.dart';
import 'dart:async';

class _CountdownTimerPageState extends State<CountdownTimerPage> {
  Timer _timer;
  int _remainingSeconds = 10;

  @override
  void initState() {
    super.initState();
    startTimer();
  }

  @override
  void dispose() {
    _timer.cancel();
    super.dispose();
  }

  void startTimer() {
    _timer = Timer.periodic(Duration(seconds: 1), (timer) {
      setState(() {
        if (_remainingSeconds > 0) {
          _remainingSeconds--;
        } else {
          _timer.cancel();
        }
      });
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Countdown Timer'),
      ),
      body: Center(
        child: Text(
          '$_remainingSeconds seconds',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

## Step 4: Implement Responsive Behaviour using MediaQuery

To make the countdown timer responsive, we will utilize `MediaQuery` to dynamically adjust the font size based on the screen size. Update the `build()` method of the `_CountdownTimerPageState` class as follows:

```dart
@override
Widget build(BuildContext context) {
  var screenWidth = MediaQuery.of(context).size.width;
  var fontSize = screenWidth * 0.1;

  return Scaffold(
    appBar: AppBar(
      title: Text('Countdown Timer'),
    ),
    body: Center(
      child: Text(
        '$_remainingSeconds seconds',
        style: TextStyle(fontSize: fontSize),
      ),
    ),
  );
}
```

## Step 5: Run the Application

Save the changes and run the Flutter application using the following command:

```dart
flutter run
```

You should now see a countdown timer that resizes itself based on the screen size. As the timer counts down, the font size adjusts automatically. Feel free to experiment with different screen sizes and orientations to see the responsiveness in action.

That's it! You have successfully created a responsive countdown timer using `MediaQuery` in Flutter. You can further enhance the timer by adding custom styles, animations, or additional functionality. Happy coding!

#flutter #responsive #countdowntimer
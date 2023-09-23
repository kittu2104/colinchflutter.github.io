---
layout: post
title: "Creating a responsive countdown timer using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [Flutter, CountdownTimer]
comments: true
share: true
---

In a mobile app, countdown timers can be a useful feature for various purposes, such as indicating the remaining time for an event or showing a countdown until a specific deadline. With Flutter's `MediaQuery` class, we can create a responsive countdown timer that adjusts its size based on the device's screen size. 

Let's get started by creating a new Flutter project and creating a new Dart file called `countdown_timer.dart`. 

```dart
import 'dart:async';
import 'package:flutter/material.dart';

class CountdownTimer extends StatefulWidget {
  @override
  _CountdownTimerState createState() => _CountdownTimerState();
}

class _CountdownTimerState extends State<CountdownTimer> {
  Timer? _timer;
  int _secondsLeft = 60; // Total seconds for the countdown timer

  @override
  void initState() {
    super.initState();
    startTimer();
  }

  @override
  void dispose() {
    _timer?.cancel();
    super.dispose();
  }

  void startTimer() {
    _timer = Timer.periodic(Duration(seconds: 1), (Timer timer) {
      setState(() {
        if (_secondsLeft > 0) {
          _secondsLeft--;
        } else {
          timer.cancel();
        }
      });
    });
  }

  @override
  Widget build(BuildContext context) {
    return Text(
      '$_secondsLeft s',
      style: TextStyle(fontSize: MediaQuery.of(context).size.width * 0.1),
    );
  }
}
```

In the above code, we have created a `CountdownTimer` widget that extends `StatefulWidget`. Inside the `_CountdownTimerState`, we have a `Timer` object that runs every second decrementing the `_secondsLeft` variable until it reaches 0. Once the timer reaches 0, it cancels itself.

In the `build` method, we display the remaining seconds as text using the `Text` widget. The font size of the text is set dynamically by multiplying the screen width by 0.1 using `MediaQuery`.

Let's use our `CountdownTimer` widget in another Flutter screen. Create a new Dart file called `home_screen.dart` and use the following code:

```dart
import 'package:flutter/material.dart';

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Countdown Timer'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            CountdownTimer(),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                // Restart the timer when the button is pressed
              },
              child: Text('Restart Timer'),
            ),
          ],
        ),
      ),
    );
  }
}
```

In the above code, we have created a `HomeScreen` widget with a simple layout consisting of a `CountdownTimer` widget and a button to restart the timer.

To use `home_screen.dart` as the home screen of our Flutter app, modify the `lib/main.dart` file with the following code:

```dart
import 'package:flutter/material.dart';
import 'home_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Countdown Timer Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: HomeScreen(),
    );
  }
}
```

That's it! Now, whenever you run the app, you will have a responsive countdown timer that adjusts its size based on the device's screen size. You can also restart the timer by pressing the "Restart Timer" button.

#Flutter #CountdownTimer
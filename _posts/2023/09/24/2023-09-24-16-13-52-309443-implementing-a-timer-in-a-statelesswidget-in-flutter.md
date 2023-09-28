---
layout: post
title: "Implementing a timer in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [timer]
comments: true
share: true
---

In this blog post, we will discuss how to implement a timer in a `StatelessWidget` in Flutter. A timer is a common component in many applications, and it is useful for displaying countdowns, measuring durations, or triggering actions after a specific interval. 

To implement a timer, we will use the `Timer` class from the `dart:async` package. The `Timer` class provides a simple way to execute a function after a specified duration.

## Steps to Implement a Timer

### Step 1: Import the required packages

To use the `Timer` class, we need to import the `dart:async` package. Open your editor and add the following import statement at the top of your file:

```dart
import 'dart:async';
```

### Step 2: Create a StatefulWidget

To include a timer logic in our `StatelessWidget`, we need to wrap it with a `StatefulWidget`. Create a new file called `timer_widget.dart`, and add the following code:

```dart
import 'dart:async';

import 'package:flutter/material.dart';

class TimerWidget extends StatefulWidget {
  @override
  _TimerWidgetState createState() => _TimerWidgetState();
}

class _TimerWidgetState extends State<TimerWidget> {
  Timer _timer;
  int _seconds = 0;

  @override
  void initState() {
    _startTimer();
    super.initState();
  }

  void _startTimer() {
    const oneSec = Duration(seconds: 1);
    _timer = Timer.periodic(oneSec, (Timer timer) {
      setState(() {
        _seconds++;
      });
    });
  }

  @override
  void dispose() {
    _timer.cancel();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Text('Timer: $_seconds seconds');
  }
}
```

In the above code, we create a basic `StatefulWidget` called `TimerWidget`. We initialize the `_seconds` variable to hold the number of seconds elapsed. In the `initState` method, we start the timer by calling the `_startTimer` method. The `_startTimer` method creates a new `Timer` that fires every second, incrementing the `_seconds` count and triggering a UI update via the `setState` method.

We also override the `dispose` method to cancel the timer when the widget is disposed of, to avoid memory leaks.

### Step 3: Use TimerWidget in your application

Now that we have our `TimerWidget` ready, we can use it in our application. In your main application file (usually `main.dart`), import the `timer_widget.dart` file and add the `TimerWidget` to your widget tree.

```dart
import 'package:flutter/material.dart';
import 'timer_widget.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Timer Example',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Timer Example'),
        ),
        body: Center(
          child: TimerWidget(),
        ),
      ),
    );
  }
}
```

In the above example, we create a simple Flutter application with a `MyApp` widget that uses the `TimerWidget` as the main content of the page.

### Conclusion

In this blog post, we learned how to implement a timer in a `StatelessWidget` in Flutter. We used the `Timer` class to create a simple timer that updates the UI every second. By following the steps outlined in this guide, you can easily include a timer component in your Flutter application.

#flutter #timer
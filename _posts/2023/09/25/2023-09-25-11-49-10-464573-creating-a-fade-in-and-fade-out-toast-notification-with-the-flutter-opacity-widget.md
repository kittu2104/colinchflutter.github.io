---
layout: post
title: "Creating a fade-in and fade-out toast notification with the Flutter Opacity widget"
description: " "
date: 2023-09-25
tags: [toastnotification]
comments: true
share: true
---

## Introduction
In Flutter, toast notifications are an effective way to provide feedback or display important messages to users. One way to enhance the user experience is to animate the appearance and disappearance of toast notifications. In this tutorial, we will learn how to create a fade-in and fade-out effect for toast notifications using the Flutter Opacity widget.

## Prerequisites
- Basic knowledge of Flutter and Dart programming language.
- Flutter SDK set up on your development machine.
- A code editor of your choice.

## Implementation

### Step 1: Set up a new Flutter project
Create a new Flutter project using the following command:

```bash
$ flutter create toast_notification
$ cd toast_notification
```

### Step 2: Update the pubspec.yaml file
Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter

  fluttertoast: ^8.0.7
```

Save the file and run the following command to download the dependencies:

```bash
$ flutter pub get
```

### Step 3: Create the toast notification widget
In the `lib` directory, create a new file called `toast_notification.dart`. Open the file and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:fluttertoast/fluttertoast.dart';

class ToastNotification extends StatefulWidget {
  final String message;

  ToastNotification({required this.message});

  @override
  _ToastNotificationState createState() => _ToastNotificationState();
}

class _ToastNotificationState extends State<ToastNotification>
    with TickerProviderStateMixin {
  late AnimationController _fadeInController;
  late Animation<double> _fadeInAnimation;

  @override
  void initState() {
    super.initState();

    _fadeInController = AnimationController(
      duration: const Duration(milliseconds: 300),
      vsync: this,
    );

    _fadeInAnimation = CurveTween(curve: Curves.easeIn).animate(_fadeInController);

    _fadeInController.forward();

    _fadeInController.addStatusListener((status) {
      if (status == AnimationStatus.completed) {
        _fadeOut();
      }
    });
  }

  void _fadeOut() async {
    await Future.delayed(Duration(milliseconds: 2000));

    _fadeInController.reverse().then((value) {
      Navigator.of(context).pop();
    });
  }

  @override
  Widget build(BuildContext context) {
    Size screenSize = MediaQuery.of(context).size;

    return FadeTransition(
      opacity: _fadeInAnimation,
      child: Container(
        width: screenSize.width * 0.8,
        padding: const EdgeInsets.symmetric(vertical: 12, horizontal: 16),
        decoration: BoxDecoration(
          color: Colors.black.withOpacity(0.8),
          borderRadius: BorderRadius.circular(8),
        ),
        child: Text(
          widget.message,
          style: const TextStyle(color: Colors.white),
        ),
      ),
    );
  }

  @override
  void dispose() {
    _fadeInController.dispose();
    super.dispose();
  }
}
```

### Step 4: Display the toast notification
In your main application file (`lib/main.dart`), add the following code to display the toast notification:

```dart
import 'package:flutter/material.dart';
import 'package:toast_notification/toast_notification.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Toast Notification Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    void showToast(BuildContext context) {
      showGeneralDialog(
        context: context,
        barrierDismissible: true,
        barrierColor: Colors.black.withOpacity(0.5),
        pageBuilder: (_, __, ___) {
          return Align(
            alignment: Alignment.bottomCenter,
            child: Padding(
              padding: const EdgeInsets.only(bottom: 24),
              child: ToastNotification(message: 'This is a toast notification'),
            ),
          );
        },
      );
    }

    return Scaffold(
      appBar: AppBar(
        title: const Text('Toast Notification Example'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            showToast(context);
          },
          child: const Text('Show Toast'),
        ),
      ),
    );
  }
}
```

### Step 5: Run the application
Save the file and run the app using the following command:

```bash
$ flutter run
```

Now, when you tap the "Show Toast" button, a toast notification with a fade-in and fade-out effect will appear and disappear after a few seconds.

## Conclusion
In this tutorial, we learned how to create a fade-in and fade-out effect for toast notifications in Flutter using the Opacity widget. By applying animations to toast notifications, we can provide a more visually appealing and interactive experience for our users.

#flutter #toastnotification
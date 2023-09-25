---
layout: post
title: "Creating a fade-in and fade-out text animation with the Flutter Opacity widget"
description: " "
date: 2023-09-25
tags: [animation]
comments: true
share: true
---

In this tutorial, we will learn how to create a fade-in and fade-out text animation using the Flutter framework. We will achieve this effect by manipulating the opacity of the text widget using the `Opacity` widget provided by Flutter.

### Prerequisites

Make sure you have Flutter and Dart installed on your development environment. If not, you can find the installation instructions on the [official Flutter website](https://flutter.dev).

### Step 1: Set up a Flutter project

Create a new Flutter project by running the following command in your terminal:

```bash
flutter create fade_in_out_text_animation
```

Move into the project directory:

```bash
cd fade_in_out_text_animation
```

### Step 2: Modify the main.dart file

Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';

void main() {
  runApp(FadeInOutTextAnimationApp());
}

class FadeInOutTextAnimationApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Fade-In Out Text Animation',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: FadeInOutTextAnimationPage(),
    );
  }
}

class FadeInOutTextAnimationPage extends StatefulWidget {
  @override
  _FadeInOutTextAnimationPageState createState() =>
      _FadeInOutTextAnimationPageState();
}

class _FadeInOutTextAnimationPageState extends State<FadeInOutTextAnimationPage>
    with SingleTickerProviderStateMixin {
  AnimationController _animationController;
  Animation<double> _opacityAnimation;

  @override
  void initState() {
    super.initState();

    _animationController = AnimationController(
      vsync: this,
      duration: Duration(seconds: 2),
    )..repeat(reverse: true);

    _opacityAnimation = Tween(begin: 0.0, end: 1.0).animate(
        CurvedAnimation(parent: _animationController, curve: Curves.easeInOut));
  }

  @override
  void dispose() {
    _animationController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Fade-In Out Text Animation'),
      ),
      body: Center(
        child: AnimatedBuilder(
          animation: _opacityAnimation,
          builder: (BuildContext context, Widget child) {
            return Opacity(
              opacity: _opacityAnimation.value,
              child: Text(
                'Hello, Flutter!',
                style: TextStyle(fontSize: 24),
              ),
            );
          },
        ),
      ),
    );
  }
}
```

### Step 3: Run the app

Save the changes made in the `main.dart` file and run the app using the following command:

```bash
flutter run
```

Congratulations! You have successfully created a Flutter app with a fade-in and fade-out text animation using the `Opacity` widget. Play around with the duration and styling of the text to create your desired effect.

#flutter #animation
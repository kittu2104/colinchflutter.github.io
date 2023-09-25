---
layout: post
title: "Creating a progressive fade-in effect with the Opacity widget"
description: " "
date: 2023-09-25
tags: [Flutter, FadeInEffect]
comments: true
share: true
---

In this tutorial, we will learn how to create a progressive fade-in effect using the Opacity widget in a Flutter application. The Opacity widget allows us to control the opacity of its child widget, ranging from fully invisible (0.0) to fully visible (1.0). By gradually increasing the opacity, we can achieve a smooth fade-in effect.

## Prerequisites:
- Basic knowledge of Flutter and Dart
- Flutter SDK installed

Let's get started!

### 1. Create a new Flutter project

Open your terminal and run the following command to create a new Flutter project:

```dart
flutter create fade_in_effect
```

### 2. Setting up the project

Navigate to the newly created project directory:

```dart
cd fade_in_effect
```

Open the `lib/main.dart` file in your preferred text editor and replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Fade In Effect',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: FadeInEffect(),
    );
  }
}

class FadeInEffect extends StatefulWidget {
  @override
  _FadeInEffectState createState() => _FadeInEffectState();
}

class _FadeInEffectState extends State<FadeInEffect>
    with SingleTickerProviderStateMixin {
  AnimationController _animationController;
  Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _animationController = AnimationController(
      vsync: this,
      duration: Duration(seconds: 1),
    );

    _animation = CurvedAnimation(
      parent: _animationController,
      curve: Curves.easeIn,
    );

    _animationController.forward();
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
        title: Text('Fade-In Effect'),
      ),
      body: Center(
        child: FadeTransition(
          opacity: _animation,
          child: FlutterLogo(
            size: 200,
          ),
        ),
      ),
    );
  }
}
```

### 3. Run the application

Save the changes to the `main.dart` file and run the app using the following command:

```dart
flutter run
```

The app should start and display a fade-in effect with a Flutter logo gradually fading in. The animation is controlled by the `AnimationController` and `CurvedAnimation` classes.

### Conclusion

In this tutorial, we learned how to create a progressive fade-in effect using the Opacity widget in Flutter. By manipulating the opacity value over time, we were able to achieve a smooth fade-in animation. Feel free to customize the duration, curve, and child widget to create unique fade-in effects in your Flutter applications.

Happy coding!

#Flutter #FadeInEffect
---
layout: post
title: "Using the TweenSequence widget with the Opacity widget for sequence fade-in animations"
description: " "
date: 2023-09-25
tags: [flutter, animations]
comments: true
share: true
---

Fade-in animations are a great way to add visual interest and enhance the user experience of your app. In Flutter, we can easily create fade-in animations using the `TweenSequence` widget combined with the `Opacity` widget. This powerful combination allows us to define a sequence of fade-in animations with different durations and easing curves.

To get started, make sure you have the Flutter SDK installed on your machine. Then, create a new Flutter project using the following command:

```dart
flutter create fade_in_animation
```

Now, let's dive into the implementation details.

## Step 1: Import the required packages

First, open the `pubspec.yaml` file of your Flutter project and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter

  animated_text_kit: ^4.2.1
```

After adding the dependencies, run the following command to fetch the packages:

```dart
flutter pub get
```

## Step 2: Create a `TweenSequence` instance

Next, open the `main.dart` file and import the required packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/scheduler.dart' show timeDilation;
```

Inside the `MyApp` widget, create a `TweenSequence` instance that defines the fade-in animations:

```dart
final _fadeAnimation = TweenSequence([
  TweenSequenceItem<double>(
    tween: Tween<double>(begin: 0.0, end: 1.0)
        .chain(CurveTween(curve: Curves.easeInOut)),
    weight: 1.0,
  ),
  TweenSequenceItem<double>(
    tween: Tween<double>(begin: 0.0, end: 1.0)
        .chain(CurveTween(curve: Curves.easeInOut)),
    weight: 1.0,
  ),
  TweenSequenceItem<double>(
    tween: Tween<double>(begin: 0.0, end: 1.0)
        .chain(CurveTween(curve: Curves.easeInOut)),
    weight: 1.0,
  ),
]);
```

In the code above, we define three `TweenSequenceItem` objects, each with a different easing curve. The `weight` property determines the duration of each animation relative to the others.

## Step 3: Create the UI with the `Opacity` widget

Now, create a simple UI that demonstrates the fade-in animation. Wrap the UI elements that you want to animate in an `Opacity` widget and connect it with the `TweenSequence` animation using a `Builder` widget:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    body: Center(
      child: AnimatedBuilder(
        animation: _fadeAnimation,
        builder: (context, child) {
          return Opacity(
            opacity: _fadeAnimation.evaluate(AlwaysStoppedAnimation(1.0)),
            child: Text(
              'Fade-In Animation',
              style: TextStyle(fontSize: 24.0),
            ),
          );
        },
      ),
    ),
  );
}
```

In the above example, we are animating the opacity of the `Text` widget using the `_fadeAnimation`. The `opacity` value is obtained by evaluating the `_fadeAnimation` with an `AlwaysStoppedAnimation` of 1.0.

## Step 4: Run the app

Save the changes and run the app using the following command:

```dart
flutter run
```

You should now see a fade-in animation applied to the text. Experiment with different durations and easing curves to achieve the desired effect.

## Conclusion

In this tutorial, we explored how to create fade-in animations using the `TweenSequence` widget with the `Opacity` widget in Flutter. By defining a sequence of animations with different durations and easing curves, we can bring our UI to life and provide a more engaging user experience.

#flutter #animations
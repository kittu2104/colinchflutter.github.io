---
layout: post
title: "Implementing responsive swipeable cards using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [ResponsiveSwipeableCards]
comments: true
share: true
---

In this tutorial, we will learn how to implement responsive swipeable cards in Flutter using `MediaQuery`. Swipeable cards are a common UI pattern in many mobile apps, where users can swipe left or right to perform actions on individual cards. By making the cards responsive, we ensure that they look and function well on different screen sizes and orientations.

## Prerequisites

Before we get started, make sure you have Flutter and Dart installed on your machine. You should also have a basic understanding of Flutter widgets and layout concepts.

## Step 1: Set up a Flutter project

Create a new Flutter project using the command line or your preferred IDE. This can be done using the following command: 

```bash
flutter create swipeable_cards
```

## Step 2: Add dependencies

Open the `pubspec.yaml` file in your project and add the following dependencies:

```yaml
dependencies:
  flutter_swipeable: ^0.9.2
```

Save the file and run `flutter pub get` to fetch the new dependencies.

## Step 3: Create a SwipeableCard Widget

Create a new Dart file called `swipeable_card.dart` and define a new stateless widget called `SwipeableCard`. This widget will represent a single swipeable card in our app.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_swipeable/flutter_swipeable.dart';

class SwipeableCard extends StatelessWidget {
  final Widget child;
  final Function() onSwipeLeft;
  final Function() onSwipeRight;

  const SwipeableCard({
    required this.child,
    required this.onSwipeLeft,
    required this.onSwipeRight,
  });

  @override
  Widget build(BuildContext context) {
    return Swipeable(
      child: child,
      onSwipeLeft: onSwipeLeft,
      onSwipeRight: onSwipeRight,
    );
  }
}
```

In this code, we've created a `SwipeableCard` widget that takes three parameters: `child` representing the contents of the card, `onSwipeLeft` and `onSwipeRight` representing the callback functions to be executed when the card is swiped left or right.

We wrap the `child` widget with the `Swipeable` widget from the `flutter_swipeable` package. This widget handles the swipe gestures and triggers the appropriate callbacks.

## Step 4: Implement a Swipeable Card Screen

In the main application file, replace the code in the `MyApp` class with the following code:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Swipeable Cards',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: SwipeableCardScreen(),
    );
  }
}

class SwipeableCardScreen extends StatefulWidget {
  @override
  _SwipeableCardScreenState createState() => _SwipeableCardScreenState();
}

class _SwipeableCardScreenState extends State<SwipeableCardScreen> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Swipeable Cards'),
      ),
      body: ListView.builder(
        itemCount: 10,
        itemBuilder: (context, index) {
          return SwipeableCard(
            child: ListTile(
              title: Text('Card $index'),
            ),
            onSwipeLeft: () {
              print('Swiped left on card $index');
            },
            onSwipeRight: () {
              print('Swiped right on card $index');
            },
          );
        },
      ),
    );
  }
}
```

Here, we've defined a new stateful widget called `SwipeableCardScreen` that represents the screen where swipeable cards are shown. 

Inside the `ListView.builder`, we create multiple `SwipeableCard` widgets with a `ListTile` as the child. The `onSwipeLeft` and `onSwipeRight` callbacks are defined to print an informational message on the console when a card is swiped left or right.

## Step 5: Running the App

Save the changes and run the app using your preferred method (`flutter run` command, IDE, etc.). You should see a screen with swipeable cards listed, and the console should log the swiping actions as you swipe the cards left or right.

## Conclusion

By implementing responsive swipeable cards using `MediaQuery` in Flutter, you can provide an engaging user experience across different screen sizes and orientations. You can further customize the cards by adding animations or actions in the swipe callbacks. Happy coding!

## #Flutter #ResponsiveSwipeableCards
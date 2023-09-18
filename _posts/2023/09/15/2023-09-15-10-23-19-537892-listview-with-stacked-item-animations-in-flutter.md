---
layout: post
title: "ListView with stacked item animations in Flutter."
description: " "
date: 2023-09-15
tags: [animation]
comments: true
share: true
---

In Flutter, the ListView widget is commonly used for displaying a list of items. However, sometimes we might want to add more visual effects to make the list more engaging and attractive. One such effect is stacked item animations, where each item in the list appears to stack on top of the previous one with a slight delay and animation.

In this tutorial, we will explore how to implement stacked item animations in a ListView in Flutter. Let's get started!

## Setting up the project

First, let's create a new Flutter project using the following command:

```dart
flutter create stacked_list_animation
```

Navigate to the project directory:

```dart
cd stacked_list_animation
```

Now, open `lib/main.dart` in your favorite code editor.

## Implementing stacked item animations

1. Import the required Flutter packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/scheduler.dart';
```

2. Create a list of items that you want to display in the ListView. Each item should be a separate widget.

```dart
List<Widget> itemList = [
  ItemWidget(color: Colors.blue, number: '1'),
  ItemWidget(color: Colors.green, number: '2'),
  ItemWidget(color: Colors.red, number: '3'),
  // Add more items as needed
];
```

3. Create a StatefulWidget class called `StackedListAnimation` that will handle the animation logic.

```dart
class StackedListAnimation extends StatefulWidget {
  @override
  _StackedListAnimationState createState() => _StackedListAnimationState();
}

class _StackedListAnimationState extends State<StackedListAnimation> with SingleTickerProviderStateMixin {
  AnimationController _animationController;
  final double _itemSpacing = 20.0;
  final int _animationDuration = 500;

  @override
  void initState() {
    super.initState();
    _animationController = AnimationController(
      duration: Duration(milliseconds: _animationDuration),
      vsync: this,
    );
    _startAnimation();
  }

  @override
  void dispose() {
    _animationController.dispose();
    super.dispose();
  }

  void _startAnimation() {
    _animationController.reset();
    _animationController.forward();
  }

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: itemList.length,
      itemBuilder: (BuildContext context, int index) {
        return SlideTransition(
          position: Tween<Offset>(
            begin: Offset(0, index * _itemSpacing),
            end: Offset(0, 0),
          ).animate(
            CurvedAnimation(
              parent: _animationController,
              curve: Interval(
                (index / itemList.length) * 0.5,
                1.0,
                curve: Curves.easeOut,
              ),
            ),
          ),
          child: itemList[index],
        );
      },
    );
  }
}
```

4. Create a separate widget class for your item. In this example, we will create an `ItemWidget` class.

```dart
class ItemWidget extends StatelessWidget {
  final Color color;
  final String number;

  ItemWidget({this.color, this.number});

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 100,
      color: color,
      child: Center(
        child: Text(
          number,
          style: TextStyle(fontSize: 24, color: Colors.white),
        ),
      ),
    );
  }
}
```

5. Finally, modify the `build` method of your `main.dart` file to use the `StackedListAnimation` widget.

```dart
void main() {
  runApp(StackedListViewApp());
}

class StackedListViewApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: StackedListAnimation(),
      ),
    );
  }
}
```

## Running the app

Save the changes and run the app using the following command:

```dart
flutter run
```

You should now see the list of items appearing in a stacked manner with a smooth animation.

## Conclusion

In this tutorial, we learned how to implement stacked item animations in a ListView using Flutter. By applying this technique, you can make your lists more visually appealing and interactive for your users. Feel free to experiment with different animation durations and curves to achieve the desired effect for your app.

#flutter #animation
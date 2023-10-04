---
layout: post
title: "Working with animations and transitions using GetX in Flutter"
description: " "
date: 2023-09-29
tags: [GetX, Animations, Transitions]
comments: true
share: true
---

GetX is a lightweight package that provides a range of utilities for state management, routing, and more. It also includes powerful tools for animating widgets and creating smooth transitions between screens.

## Getting Started

To get started with GetX animations, you need to add the package to your `pubspec.yaml` file:

```
dependencies:
  flutter:
    sdk: flutter
  get: ^4.3.8
```

## Creating Animations

With GetX, you can create animations using the `GetXController` class and the `GetX` widget. Let's start by creating a simple animation using the `GetXController` class:

```dart
import 'package:get/get.dart';

class MyAnimationController extends GetxController with SingleGetTickerProviderMixin {
  AnimationController animationController;

  @override
  void onInit() {
    super.onInit();
    animationController = AnimationController(
      duration: Duration(seconds: 2),
      vsync: this,
    );
  }

  @override
  void onClose() {
    animationController.dispose();
    super.onClose();
  }
}
```

In the above code, we extend the `GetXController` class and mix in the `SingleGetTickerProviderMixin` to provide the ticker for our animation. We initialize an `AnimationController` with a specified duration and `vsync` parameter.

## Controlling Animations

Now, let's see how we can control the animation using a button press. We'll use the `GetX` widget together with the `Obx` widget to update the animation value:

```dart
class MyAnimationController extends GetxController with SingleGetTickerProviderMixin {
  AnimationController animationController;
  Animation<double> animation;

  @override
  void onInit() {
    super.onInit();
    animationController = AnimationController(
      duration: Duration(seconds: 2),
      vsync: this,
    );
    animation = Tween<double>(begin: 0, end: 1).animate(animationController);
  }

  void playAnimation() {
    animationController.forward();
  }

  void reverseAnimation() {
    animationController.reverse();
  }

  @override
  void onClose() {
    animationController.dispose();
    super.onClose();
  }
}
```

In the updated code above, we create a `Tween` to define the animation range, and we animate the `animationController` using the `forward()` and `reverse()` methods.

## Integrating Animations in Widgets

To integrate the animation into a widget, we can use the `Obx` widget to observe the animation value and update the UI accordingly:

```dart
class MyHomePage extends StatelessWidget {
  final MyAnimationController _myAnimationController = Get.put(MyAnimationController());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Animation Example'),
      ),
      body: Center(
        child: Obx(
          () => Opacity(
            opacity: _myAnimationController.animation.value,
            child: Container(
              width: 200,
              height: 200,
              color: Colors.blue,
            ),
          ),
        ),
      ),
      floatingActionButton: Row(
        mainAxisAlignment: MainAxisAlignment.end,
        children: [
          FloatingActionButton(
            onPressed: _myAnimationController.playAnimation,
            child: Icon(Icons.play_arrow),
          ),
          SizedBox(width: 10),
          FloatingActionButton(
            onPressed: _myAnimationController.reverseAnimation,
            child: Icon(Icons.stop),
          ),
        ],
      ),
    );
  }
}
```

In the code above, we observe the `animation` value using the `Obx` widget and apply the `opacity` value to the `Container` widget.

## Conclusion

Using GetX in Flutter makes implementing animations and transitions simpler and more efficient. GetX provides a clean and intuitive way to control animations and integrate them into your app's UI. Give it a try and take your app's user experience to the next level!

#Flutter #GetX #Animations #Transitions
---
layout: post
title: "Using GetX for state persistence in Flutter"
description: " "
date: 2023-09-29
tags: [flutter, statepersistence]
comments: true
share: true
---

![GetX](https://miro.medium.com/max/1000/1*i1CuWxJYZ5HrHp10P6oUHQ.png)

State management is an essential aspect of any mobile development framework. In Flutter, there are several popular state management solutions available, and one of them is **GetX**. GetX is a powerful, lightweight, and flexible state management package that makes it easy to handle state persistence in Flutter.

In this tutorial, we will explore how to use GetX for state persistence in a Flutter application.

## Installation

To use GetX in your Flutter project, add the following dependency to your `pubspec.yaml` file:

```dart
dependencies:
  get: ^4.1.4
```

Then, run `flutter pub get` to fetch the package.

## Setting up the State

To get started with GetX for state persistence, make sure you have a model or class that represents the state you want to persist. Let's say we have a simple `Counter` class with a `count` property:

```dart
class Counter {
  int count = 0;
  
  void increment() {
    count++;
  }
  
  void decrement() {
    count--;
  }
}
```

## Creating a Controller

Next, we need to create a controller class that will be responsible for managing the state persistence using GetX. The controller will have a reference to the model and will define methods to update the state.

```dart
import 'package:get/get.dart';

class CounterController extends GetxController {
  final Counter counter = Counter();

  void increment() {
    counter.increment();
    update(); // Notify GetX that the state has changed
  }

  void decrement() {
    counter.decrement();
    update(); // Notify GetX that the state has changed
  }
}
```

## Using the Controller

Now, we can use the `CounterController` in our Flutter widget to manage the state. We can access the state in the widget using the `GetBuilder` widget from GetX.

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

class HomePage extends StatelessWidget {
  final CounterController controller = Get.put(CounterController());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('GetX State Persistence Example'),
      ),
      body: Center(
        child: GetBuilder<CounterController>(
          builder: (controller) {
            return Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Text(
                  'Count: ${controller.counter.count}',
                  style: TextStyle(fontSize: 24),
                ),
                SizedBox(height: 16),
                ElevatedButton(
                  onPressed: () => controller.increment(),
                  child: Text('Increment'),
                ),
                ElevatedButton(
                  onPressed: () => controller.decrement(),
                  child: Text('Decrement'),
                ),
              ],
            );
          },
        ),
      ),
    );
  }
}
```

## Conclusion

Using GetX for state persistence in Flutter is a simple and effective way to manage and persist state in your application. GetX provides a convenient and intuitive API for handling state changes and updating UI components. With just a few lines of code, you can have a robust state management system in your Flutter app.

Give GetX a try and experience the power of state persistence in your Flutter projects!

#flutter #statepersistence
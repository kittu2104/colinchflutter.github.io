---
layout: post
title: "Creating a responsive stepper navigation using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [responsive]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive stepper navigation using `MediaQuery` in Flutter. Steppers are commonly used in mobile applications to guide users through a series of steps or actions.

## Step 1: Setting up the Flutter project
Before we begin, make sure that you have Flutter installed on your machine and have set up a new Flutter project. If you haven't, you can follow the official Flutter installation guide [here](https://flutter.dev/docs/get-started/install).

## Step 2: Adding necessary dependencies
Open your project's `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter

  percent_indicator: ^3.0.1
```

Save the file and run `flutter pub get` to download and install the dependencies.

## Step 3: Creating the stepper widget
Create a new file, `stepper_widget.dart`, and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:percent_indicator/percent_indicator.dart';

class StepperWidget extends StatelessWidget {
  final int currentIndex;
  final int totalSteps;

  const StepperWidget({required this.currentIndex, required this.totalSteps});

  @override
  Widget build(BuildContext context) {
    final double screenWidth = MediaQuery.of(context).size.width;
    final double progress = (currentIndex + 1) / totalSteps;

    return Padding(
      padding: const EdgeInsets.symmetric(vertical: 16.0),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          LinearPercentIndicator(
            width: screenWidth - 32,
            lineHeight: 8.0,
            percent: progress,
            progressColor: Theme.of(context).primaryColor,
          ),
          SizedBox(height: 8.0),
          Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: List.generate(
              totalSteps,
              (index) => Container(
                width: (screenWidth - 32) / totalSteps,
                height: 8.0,
                decoration: BoxDecoration(
                  color: index <= currentIndex
                      ? Theme.of(context).primaryColor
                      : Theme.of(context).disabledColor,
                ),
              ),
            ),
          ),
        ],
      ),
    );
  }
}
```

In the above code, we create a stateless widget `StepperWidget` which takes two required parameters: `currentIndex` and `totalSteps`. Inside the `build` method, we use `MediaQuery` to get the screen width and calculate the progress percentage. We then use the `LinearPercentIndicator` from the `percent_indicator` package to display a progress bar. Additionally, we display individual steps as containers with different colors based on the current step.

## Step 4: Using the stepper widget
In the file where you want to use the stepper widget, import the `stepper_widget.dart` file and add the following code:

```dart
import 'package:flutter/material.dart';
import 'stepper_widget.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Stepper Navigation'),
      ),
      body: Center(
        child: StepperWidget(currentIndex: 2, totalSteps: 4),
      ),
    );
  }
}

void main() {
  runApp(MyApp());
}
```

In the above code, we simply use the `StepperWidget` in the `body` of our `MyApp` widget. We can specify the `currentIndex` and `totalSteps` to indicate the current step and the total number of steps, respectively.

## Conclusion
In this tutorial, we learned how to create a responsive stepper navigation using `MediaQuery` in Flutter. By using the `percent_indicator` package and customizing the appearance of each step, we can provide users with a visually engaging and intuitive navigation experience.

Remember to check the official Flutter documentation for more information on `MediaQuery` and other Flutter features.

Happy coding! #flutter #responsive
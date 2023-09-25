---
layout: post
title: "Creating a custom progress stepper using CustomClipper in Flutter"
description: " "
date: 2023-09-21
tags: [customstepper]
comments: true
share: true
---

In this tutorial, we will learn how to create a custom progress stepper using the CustomClipper widget in Flutter. A progress stepper is a common UI element used to show the progress of a multi-step process, such as a form submission or a payment flow. By using CustomClipper, we can achieve a custom and visually appealing design for our progress stepper.

## Step 1: Setting up the Project

First, let's start by creating a new Flutter project. Open your terminal or command prompt and navigate to the desired directory. Run the following command:

```shell
flutter create custom_progress_stepper
```

## Step 2: Creating the Custom Clipper

Next, we need to create a custom clipper class that will define the shape of our progress stepper. Create a new file called `custom_clipper.dart` in the `lib` folder and add the following code:

```dart
import 'package:flutter/material.dart';

class ProgressStepperClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    final path = Path();
    final radius = size.height / 2;

    path.lineTo(radius, 0);
    path.arcToPoint(
      Offset(size.width - radius, 0),
      radius: Radius.circular(radius),
    );
    path.lineTo(size.width, size.height);
    path.lineTo(0, size.height);
    path.close();

    return path;
  }

  @override
  bool shouldReclip(covariant CustomClipper<Path> oldClipper) => false;
}
```

In this code, we create a custom class `ProgressStepperClipper` that extends `CustomClipper<Path>`. We override the `getClip` method to define the custom shape of the clipper. We create a rounded rectangle that represents each step of the progress stepper. The `shouldReclip` method returns false, indicating that the clipper should not be recomputed when the shape changes.

## Step 3: Implementing the Custom Progress Stepper

Now, let's implement the custom progress stepper in our main.dart file. Replace the contents of the file with the following code:

```dart
import 'package:flutter/material.dart';

import 'custom_clipper.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom Progress Stepper',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: CustomStepper(),
    );
  }
}

class CustomStepper extends StatefulWidget {
  @override
  _CustomStepperState createState() => _CustomStepperState();
}

class _CustomStepperState extends State<CustomStepper> {
  int _currentStep = 0;
  final List<String> _steps = [
    'Step 1',
    'Step 2',
    'Step 3',
    'Step 4',
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Progress Stepper'),
      ),
      body: Container(
        padding: EdgeInsets.all(20.0),
        alignment: Alignment.center,
        child: Row(
          mainAxisAlignment: MainAxisAlignment.spaceAround,
          children: _steps
              .map(
                (step) => _buildStep(
                  step,
                  _steps.indexOf(step) <= _currentStep,
                ),
              )
              .toList(),
        ),
      ),
    );
  }

  Widget _buildStep(String label, bool completed) {
    return Column(
      children: [
        Container(
          width: 60,
          height: 60,
          alignment: Alignment.center,
          child: Text(
            _steps.indexOf(label) < _currentStep ? '✓' : (completed ? '✓' : ''),
            style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
          ),
        ),
        SizedBox(height: 8.0),
        SizedBox(
          width: 100,
          child: Text(
            label,
            textAlign: TextAlign.center,
            style: TextStyle(
              fontSize: 14,
              color: _steps.indexOf(label) <= _currentStep
                  ? Colors.green
                  : Colors.grey,
              fontWeight: _steps.indexOf(label) <= _currentStep
                  ? FontWeight.bold
                  : FontWeight.normal,
            ),
          ),
        ),
      ],
    );
  }
}
```

This code sets up our custom progress stepper using the custom clipper defined in the `ProgressStepperClipper` class. We create a `CustomStepper` widget that maintains the state of the current step. We use a `Row` to display each step of the progress stepper, and the `_buildStep` method generates the UI for each step.

## Step 4: Running the App

Save the files and run the app using the following command:

```shell
flutter run
```

You should now see the custom progress stepper in the app. Each completed step will be marked with a checkmark. You can further customize the design by modifying the styles and animations to fit your app's UI.

---

Implementing a custom progress stepper using CustomClipper in Flutter allows us to create visually appealing and interactive UI elements for multi-step processes. Feel free to experiment with different shapes and designs to match the desired look and feel of your app.

#flutter #customstepper
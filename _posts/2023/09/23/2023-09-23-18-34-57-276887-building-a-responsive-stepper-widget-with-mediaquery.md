---
layout: post
title: "Building a responsive stepper widget with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [responsive, flutterdevelopment]
comments: true
share: true
---

![Responsive Stepper Widget](https://example.com/responsive-stepper-widget.jpg)

In this tutorial, we will learn how to build a responsive stepper widget using the `MediaQuery` class in Flutter. Steppers are often used in mobile applications to guide users through a series of steps. By making the stepper widget responsive, we ensure that it adapts to different screen sizes and orientations.

## Prerequisites
To follow along with this tutorial, you need to have Flutter installed on your machine. You should also have a basic understanding of Flutter widgets and layouts.

## Step 1: Set up the Flutter project
```
$ flutter create responsive_stepper_widget
$ cd responsive_stepper_widget
```

## Step 2: Create the Stepper Widget
In the `lib` folder, create a new file named `responsive_stepper.dart`. Add the following code to create a basic stepper widget:

```dart
import 'package:flutter/material.dart';

class ResponsiveStepperWidget extends StatefulWidget {
  @override
  _ResponsiveStepperWidgetState createState() => _ResponsiveStepperWidgetState();
}

class _ResponsiveStepperWidgetState extends State<ResponsiveStepperWidget> {
  int _currentStep = 0;

  List<Step> _steps = [
    Step(
      title: Text('Step 1'),
      content: Text('This is the content for Step 1.'),
      isActive: true,
    ),
    Step(
      title: Text('Step 2'),
      content: Text('This is the content for Step 2.'),
      isActive: false,
    ),
    Step(
      title: Text('Step 3'),
      content: Text('This is the content for Step 3.'),
      isActive: false,
    ),
  ];

  void _onStepContinue() {
    if (_currentStep < _steps.length - 1) {
      setState(() {
        _currentStep++;
      });
    }
  }

  void _onStepCancel() {
    if (_currentStep > 0) {
      setState(() {
        _currentStep--;
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Stepper(
      currentStep: _currentStep,
      onStepContinue: _onStepContinue,
      onStepCancel: _onStepCancel,
      steps: _steps,
    );
  }
}
```

## Step 3: Make the Stepper widget responsive
To make the stepper widget responsive, we need to determine the size of the device screen and adapt the layout accordingly. We can use the `MediaQuery` class to get the screen width and height.

Modify the `build` method of the `ResponsiveStepperWidget` as follows:

```dart
@override
  Widget build(BuildContext context) {
    double screenWidth = MediaQuery.of(context).size.width;
    double screenHeight = MediaQuery.of(context).size.height;

    bool isPortrait = screenHeight > screenWidth;

    return Container(
      child: Column(
        children: [
          if (isPortrait)
            SizedBox(height: 20),
          if (!isPortrait)
            SizedBox(height: 40),
          Stepper(
            currentStep: _currentStep,
            onStepContinue: _onStepContinue,
            onStepCancel: _onStepCancel,
            steps: _steps,
          ),
        ],
      ),
    );
```

In this modified code, we use conditional rendering to adjust the margin height of the stepper based on whether the device is in portrait or landscape orientation.

## Step 4: Integrate the Stepper widget
Now, let's integrate the `ResponsiveStepperWidget` into the main app. Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'responsive_stepper.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Stepper Widget',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive Stepper Widget'),
        ),
        body: Center(
          child: ResponsiveStepperWidget(),
        ),
      ),
    );
  }
}
```

## Step 5: Run the app
Save all the changes and run the app on an emulator or physical device:

```
$ flutter run
```

You should now see the responsive stepper widget in action. Try rotating the device to see how it adjusts to different screen sizes and orientations.

Congratulations! You have successfully built a responsive stepper widget using `MediaQuery` in Flutter. Use this knowledge to enhance the user experience and usability of your mobile applications.

#flutter #responsive #flutterdevelopment
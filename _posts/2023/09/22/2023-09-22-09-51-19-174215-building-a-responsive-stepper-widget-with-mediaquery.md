---
layout: post
title: "Building a responsive stepper widget with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [responsiveUI]
comments: true
share: true
---

In this blog post, we will explore how to build a responsive stepper widget using the `MediaQuery` class in Flutter. Stepper widgets are commonly used to guide users through a series of steps or actions. By making our stepper widget responsive, we can ensure that it adapts to different screen sizes and orientations.

## What is MediaQuery?

`MediaQuery` is a class in Flutter that provides information about the current device's screen size and pixel density. It allows us to make our UI components responsive by adjusting their layout and behavior based on the available screen space.

## Step 1: Import Required Packages

Before we get started, let's import the necessary Flutter packages:

```dart
import 'package:flutter/material.dart';
```
## Step 2: Define the Stepper Widget

Next, let's define our stepper widget. We'll create a `StatefulWidget` named `ResponsiveStepperWidget` that holds the current step index and the list of steps to display:

```dart
class ResponsiveStepperWidget extends StatefulWidget {
  @override
  _ResponsiveStepperWidgetState createState() => _ResponsiveStepperWidgetState();
}

class _ResponsiveStepperWidgetState extends State<ResponsiveStepperWidget> {
  int _currentStepIndex = 0;
  
  List<Step> _steps = [
    Step(
      title: Text('Step 1'),
      content: Text('This is step 1'),
    ),
    Step(
      title: Text('Step 2'),
      content: Text('This is step 2'),
    ),
  ];
  
  @override
  Widget build(BuildContext context) {
    return Stepper(
      currentStep: _currentStepIndex,
      steps: _steps,
      onStepContinue: () {
        setState(() {
          if (_currentStepIndex < _steps.length - 1) {
            _currentStepIndex++;
          }
        });
      },
      onStepCancel: () {
        setState(() {
          if (_currentStepIndex > 0) {
            _currentStepIndex--;
          }
        });
      },
    );
  }
}
```

## Step 3: Make the Stepper Responsive

Now, let's make our stepper widget responsive by using the `MediaQuery` class. We'll use the `MediaQuery.of(context).size` property to get the device's screen size and adjust the layout and appearance of our stepper widget accordingly.

```dart
class ResponsiveStepperWidget extends StatefulWidget {
  @override
  _ResponsiveStepperWidgetState createState() => _ResponsiveStepperWidgetState();
}

class _ResponsiveStepperWidgetState extends State<ResponsiveStepperWidget> {
  int _currentStepIndex = 0;
  
  List<Step> _steps = [
    Step(
      title: Text('Step 1'),
      content: Text('This is step 1'),
    ),
    Step(
      title: Text('Step 2'),
      content: Text('This is step 2'),
    ),
  ];
  
  @override
  Widget build(BuildContext context) {
    final screenSize = MediaQuery.of(context).size;
    
    return Container(
      width: screenSize.width > 600 ? 600 : screenSize.width,
      child: Stepper(
        currentStep: _currentStepIndex,
        steps: _steps,
        onStepContinue: () {
          setState(() {
            if (_currentStepIndex < _steps.length - 1) {
              _currentStepIndex++;
            }
          });
        },
        onStepCancel: () {
          setState(() {
            if (_currentStepIndex > 0) {
              _currentStepIndex--;
            }
          });
        },
      ),
    );
  }
}
```

## Conclusion

In this blog post, we learned how to build a responsive stepper widget using the `MediaQuery` class in Flutter. By leveraging the device's screen size, we can make our stepper adapt to different screen sizes and orientations. This ensures a consistent and user-friendly experience for our app users.

Start building your own responsive stepper widget today and enhance the usability of your Flutter app!

#flutter #responsiveUI
---
layout: post
title: "Creating a responsive stepper navigation using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [responsiveUI]
comments: true
share: true
---

In Flutter, it is important to create responsive user interfaces that adapt to different screen sizes. One common design pattern is the stepper navigation, which allows users to progress through a series of steps or pages. In this tutorial, we will learn how to create a responsive stepper navigation using the `MediaQuery` class in Flutter.

## Step 1: Set up the project

Before we start coding, let's set up a new Flutter project. Open your terminal or command prompt and run the following command:

```bash
flutter create responsive_stepper_navigation
cd responsive_stepper_navigation
```

## Step 2: Create the Stepper UI

First, let's create a new file called `stepper_page.dart` in the `lib` folder. This file will contain the UI for the stepper navigation.

```dart
import 'package:flutter/material.dart';

class StepperPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Stepper Navigation'),
      ),
      body: Column(
        children: [
          Expanded(
            child: Stepper(
              currentStep: 0,
              steps: [
                Step(
                  title: Text('Step 1'),
                  content: Container(
                    child: Text('Step 1 content'),
                  ),
                ),
                Step(
                  title: Text('Step 2'),
                  content: Container(
                    child: Text('Step 2 content'),
                  ),
                ),
                Step(
                  title: Text('Step 3'),
                  content: Container(
                    child: Text('Step 3 content'),
                  ),
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }
}
```

In this code, we define a stateless widget called `StepperPage` that displays the app bar and a `Stepper` widget. The `Stepper` widget takes an array of `Step` widgets as its `steps` property. Each `Step` widget has a `title` and `content`, which we can customize.

## Step 3: Add Responsive Behavior

Now let's make the stepper navigation responsive using the `MediaQuery` class. 

```dart
import 'package:flutter/material.dart';

class StepperPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final width = MediaQuery.of(context).size.width;

    return Scaffold(
      appBar: AppBar(
        title: Text('Stepper Navigation'),
      ),
      body: Column(
        children: [
          Expanded(
            child: Stepper(
              currentStep: 0,
              steps: [
                Step(
                  title: Text('Step 1'),
                  content: Container(
                    child: Text('Step 1 content'),
                  ),
                ),
                Step(
                  title: Text('Step 2'),
                  content: Container(
                    child: Text('Step 2 content'),
                  ),
                ),
                Step(
                  title: Text('Step 3'),
                  content: Container(
                    child: Text('Step 3 content'),
                  ),
                ),
              ],
              type: width > 600 ? StepperType.horizontal : StepperType.vertical,
            ),
          ),
        ],
      ),
    );
  }
}
```

In this updated code, we use `MediaQuery.of(context).size.width` to get the width of the current screen. We then conditionally set the `type` property of the `Stepper` widget based on the width. If the width is greater than 600, we use `StepperType.horizontal`, otherwise, we use `StepperType.vertical`.

## Conclusion

By leveraging the `MediaQuery` class in Flutter, we can easily create a responsive stepper navigation that adapts to different screen sizes. This allows our app to provide a seamless user experience on various devices.

Remember to import the necessary packages and use the code snippets provided to customize the UI and behavior of your stepper navigation.

#flutter #responsiveUI
---
layout: post
title: "Creating a responsive progress indicator using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [ResponsiveDesign]
comments: true
share: true
---

In today's tech tutorial, we will learn how to create a responsive progress indicator using `MediaQuery` in Flutter. A progress indicator is a visual representation of the progress of a task or operation. By making it responsive, we ensure that it adapts and scales properly to different device sizes and orientations.

## Getting Started

To get started, make sure you have Flutter installed on your system. If not, you can follow the official Flutter installation guide to get it set up. Once you have Flutter installed, create a new Flutter project using the following command:

```dart
flutter create responsive_progress_indicator
```

Now, open the newly created project in your preferred IDE and navigate to the `lib` directory. Inside the `lib` directory, create a new Dart file called `progress_indicator.dart`.

## Implementing the Progress Indicator

First, import the required packages:

```dart
import 'package:flutter/material.dart';
```

Create a new class called `ProgressIndicatorWidget` that extends `StatelessWidget`. This class will hold the logic and UI for our progress indicator:

```dart
class ProgressIndicatorWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: CircularProgressIndicator(),
    );
  }
}
```

In this class, we define the build method that returns a `CircularProgressIndicator` wrapped within a `Center` widget. The `CircularProgressIndicator` widget displays a spinning wheel indicating that the task is in progress.

## Making the Progress Indicator Responsive

To make the progress indicator responsive, we will use `MediaQuery` to get the size of the device's screen. We can use this information to adjust the size of the progress indicator based on the screen width.

Modify the `ProgressIndicatorWidget` class as follows:

```dart
class ProgressIndicatorWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    double screenWidth = MediaQuery.of(context).size.width;
    double indicatorSize = screenWidth * 0.2; // Adjust the size as needed

    return Center(
      child: SizedBox(
        width: indicatorSize,
        height: indicatorSize,
        child: CircularProgressIndicator(),
      ),
    );
  }
}
```

In this updated implementation, we obtained the screen width using `MediaQuery.of(context).size.width`. We then calculated the desired indicator size as a percentage of the screen width. Adjust the `indicatorSize` value according to your preferences.

By wrapping the `CircularProgressIndicator` in a `SizedBox` widget and setting the width and height to `indicatorSize`, we ensure that the progress indicator's size is responsive based on the screen width.

## Implementation Example

To use the progress indicator in your app, you can simply add it to your UI wherever you need it. For example:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive Progress Indicator'),
        ),
        body: Center(
          child: ProgressIndicatorWidget(),
        ),
      ),
    );
  }
}

class ProgressIndicatorWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    double screenWidth = MediaQuery.of(context).size.width;
    double indicatorSize = screenWidth * 0.2; // Adjust the size as needed

    return Center(
      child: SizedBox(
        width: indicatorSize,
        height: indicatorSize,
        child: CircularProgressIndicator(),
      ),
    );
  }
}
```

In this example, we added the `ProgressIndicatorWidget` as a child of the `Center` widget in the `body` of the `Scaffold`.

## Conclusion

Congratulations! You have now learned how to create a responsive progress indicator using `MediaQuery` in Flutter. By making the progress indicator responsive, you can ensure a seamless user experience across different screen sizes and orientations. Thank you for reading, and be sure to check out our other Flutter tutorials.

#Flutter #ResponsiveDesign
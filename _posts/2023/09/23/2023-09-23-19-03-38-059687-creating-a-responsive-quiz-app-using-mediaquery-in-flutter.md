---
layout: post
title: "Creating a responsive quiz app using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: []
comments: true
share: true
---

In this tutorial, we will build a responsive quiz application using `MediaQuery` in Flutter. `MediaQuery` is a powerful tool that allows us to build adaptive and responsive user interfaces in our Flutter applications. With `MediaQuery`, we can retrieve information about the device's size, orientation, and other metrics, enabling us to create responsive layouts that look great on different screen sizes.

## Step 1: Set up a Flutter project

First, make sure you have Flutter installed on your system. If not, you can follow the instructions on the official Flutter website to install it.

Create a new Flutter project by running the following command in your terminal:

```bash
$ flutter create responsive_quiz_app
```

Navigate to the project directory:

```bash
$ cd responsive_quiz_app
```

## Step 2: Set up the project structure

In this step, let's set up the basic structure of our project.

Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Quiz App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: QuizPage(),
    );
  }
}

class QuizPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Quiz'),
      ),
      body: Container(
        child: Center(
          child: Text(
            'Quiz Body',
            style: TextStyle(fontSize: 24),
          ),
        ),
      ),
    );
  }
}
```

In this code, we define a `MyApp` class that extends `StatelessWidget` and serves as the entry point of our application. Inside `MyApp`, we set up the `MaterialApp` with a title, theme, and the `QuizPage` as the initial route.

The `QuizPage` is a `StatelessWidget` that displays the basic structure of our quiz app. We have an `AppBar` with a title and a `Container` with a centered text widget as the body.

## Step 3: Make the app responsive

Now it's time to make our quiz app responsive by utilizing the `MediaQuery` class.

Inside the `QuizPage` widget, replace the `Container` with the following code:

```dart
Container(
  padding: EdgeInsets.all(16),
  child: Center(
    child: Text(
      'Quiz Body',
      style: TextStyle(fontSize: _getFontSize(context)),
    ),
  ),
)
```

Next, add the following method to the `QuizPage` class:

```dart
double _getFontSize(BuildContext context) {
  double screenWidth = MediaQuery.of(context).size.width;
  
  if (screenWidth > 600) {
    return 32;
  } else {
    return 24;
  }
}
```

In this code, we added `padding` to the `Container` to give some spacing around the quiz body. We also introduced a new `_getFontSize` method that takes the `BuildContext` as a parameter and returns a `double` value representing the font size based on the screen width. If the screen width is greater than 600 pixels, we set the font size to 32, otherwise, we use a font size of 24.

By adjusting the font size based on the screen width, our quiz app will be responsive and present an optimal user experience on different devices.

## Step 4: Test the app

To test the app, run the following command in your terminal:

```bash
$ flutter run
```

After the app builds, you should see the initial quiz page with the text displayed at a font size based on the screen width.

## Conclusion

In this tutorial, we learned how to create a responsive quiz app using `MediaQuery` in Flutter. By leveraging the power of `MediaQuery`, we can build adaptive and responsive user interfaces that work beautifully on different screen sizes. This allows us to create a seamless user experience across various devices.
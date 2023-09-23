---
layout: post
title: "Creating a responsive quiz app using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [flutter, flutterdev]
comments: true
share: true
---

In today's tech tutorial, we will learn how to create a responsive quiz app using `MediaQuery` in Flutter. `MediaQuery` is a powerful class in Flutter that allows us to obtain information about the current app's screen dimensions and orientation. By leveraging `MediaQuery`, we can create a responsive UI that adapts to different screen sizes and devices.

## Step 1: Setup

Before we dive into the implementation, make sure you have Flutter installed and set up on your machine. You can follow the official Flutter documentation to get started.

## Step 2: Project Structure

Create a new Flutter project and set up the project structure. In this example, we will have three main files:

1. `main.dart`: The entry point of our Flutter app.
2. `quiz_app.dart`: The main app widget where we will define the UI.
3. `question.dart`: A separate widget for displaying questions.

## Step 3: Implementing the Quiz App

First, let's define the structure of our quiz app. We will have a list of questions and display them one by one. Each question will have multiple choices, and the user can select one option as the answer. Once the user answers all the questions, we will calculate the final score.

In `quiz_app.dart`, start by importing the required classes:

```dart
import 'package:flutter/material.dart';
```

Next, create a new widget called `QuizApp`:

```dart
class QuizApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Quiz App'),
        ),
        body: QuestionList(), // Create a separate widget for displaying questions
      ),
    );
  }
}
```

Now, let's create the `QuestionList` widget in a separate file `question.dart`:

```dart
import 'package:flutter/material.dart';

class QuestionList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ListView(
      children: <Widget>[
        Question(title: 'Question 1', choices: ['Option 1', 'Option 2', 'Option 3']),
        Question(title: 'Question 2', choices: ['Option 1', 'Option 2', 'Option 3']),
        // Add more questions here
      ],
    );
  }
}
```

In the `Question` widget, we will display the question title and the answer choices:

```dart
class Question extends StatelessWidget {
  final String title;
  final List<String> choices;

  Question({required this.title, required this.choices});

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: EdgeInsets.all(20),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: <Widget>[
          Text(title, style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
          SizedBox(height: 10),
          Column(
            children: choices.map((choice) {
              return ListTile(
                title: Text(choice),
                onTap: () {
                  // Handle user's choice
                },
              );
            }).toList(),
          ),
        ],
      ),
    );
  }
}
```

## Step 4: Making the App Responsive

Now that we have our quiz app structure set up, let's make it responsive using `MediaQuery`. We will modify the `QuizApp` widget to adjust the layout based on the device screen size.

Update the `QuizApp` widget as follows:

```dart
class QuizApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Quiz App'),
        ),
        body: _buildBody(context), // Use a helper method to build the app's body
      ),
    );
  }

  Widget _buildBody(BuildContext context) {
    final screenWidth = MediaQuery.of(context).size.width;

    return screenWidth < 600 ? _buildMobileLayout() : _buildDesktopLayout();
  }

  Widget _buildMobileLayout() {
    return QuestionList(); // Display the list of questions in a vertical layout
  }

  Widget _buildDesktopLayout() {
    return Row(
      children: <Widget>[
        Expanded(
          flex: 2,
          child: QuestionList(),
        ),
        Expanded(
          flex: 1,
          child: Container(
            color: Colors.grey.withOpacity(0.3),
            child: Center(child: Text('Answers')),
          ),
        ),
      ],
    );
  }
}
```

In the above code, we determine the `screenWidth` using `MediaQuery` and conditionally choose between `_buildMobileLayout()` and `_buildDesktopLayout()` based on the value. On smaller screens, we display only the list of questions, while on larger screens, we display the list of questions and a column for displaying the answers.

Congratulations! You have successfully created a responsive quiz app using `MediaQuery` in Flutter. This approach allows your app to adapt to different screen sizes and provide an optimal user experience.

Now you can run your app using `flutter run` command and test it on various devices to see the responsive layout in action!

#flutter #flutterdev
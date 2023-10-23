---
layout: post
title: "Creating habit tracking and goal-setting features in MaterialApp."
description: " "
date: 2023-10-23
tags: [MaterialApp, materialapp]
comments: true
share: true
---

Tracking habits and setting goals are important aspects of personal development and self-improvement. With the help of the MaterialApp framework in Flutter, we can easily create habit tracking and goal-setting features for our mobile applications. In this blog post, we will explore how to implement these features using MaterialApp.

## Table of Contents
- [Setting up MaterialApp](#setting-up-materialapp)
- [Creating the Habit Tracking Feature](#creating-the-habit-tracking-feature)
- [Creating the Goal-Setting Feature](#creating-the-goal-setting-feature)
- [Conclusion](#conclusion)

## Setting up MaterialApp

To begin, we need to set up MaterialApp in our Flutter project. MaterialApp is a convenient way to create a consistent and responsive UI for our application. To use MaterialApp, we first need to import the necessary packages:

```dart
import 'package:flutter/material.dart';
```

Next, we can create a basic MaterialApp widget and define its properties:

```dart
void main() {
  runApp(MaterialApp(
    title: 'Habit Tracker',
    theme: ThemeData(
      // Define app theme
    ),
    home: HomePage(),
  ));
}
```

In this code snippet, we are defining the title of the application as "Habit Tracker" and setting up a custom theme for our app. We are also specifying the `HomePage` widget as the starting point of our application.

## Creating the Habit Tracking Feature

Now that we have our MaterialApp set up, we can move on to creating the habit tracking feature. Habit tracking allows users to keep track of their daily habits and monitor their progress over time.

### Creating the Habit model

First, let's create a `Habit` model class to represent the habits that users want to track:

```dart
class Habit {
  final String title;
  bool isCompleted;

  Habit({required this.title, this.isCompleted = false});
}
```

In this model class, we define the `title` of the habit and a boolean flag `isCompleted` to track whether the habit has been completed for the day.

### Implementing the Habit tracking UI

Next, we need to create the user interface to allow users to add and track their habits. We can achieve this by creating a new widget called `HabitTrackingPage`:

```dart
class HabitTrackingPage extends StatefulWidget {
  @override
  _HabitTrackingPageState createState() => _HabitTrackingPageState();
}

class _HabitTrackingPageState extends State<HabitTrackingPage> {
  List<Habit> habits = [];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Habit Tracking'),
      ),
      body: ListView.builder(
        itemCount: habits.length,
        itemBuilder: (context, index) {
          final habit = habits[index];

          return ListTile(
            title: Text(habit.title),
            trailing: Checkbox(
              value: habit.isCompleted,
              onChanged: (value) {
                setState(() {
                  habit.isCompleted = value!;
                });
              },
            ),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Add a new habit
          showDialog(
            context: context,
            builder: (context) {
              return AlertDialog(
                title: Text('Add Habit'),
                content: TextField(
                  onChanged: (value) {
                    setState(() {
                      habits.add(
                        Habit(title: value),
                      );
                    });
                  },
                ),
                actions: [
                  TextButton(
                    onPressed: () {
                      Navigator.of(context).pop();
                    },
                    child: Text('Cancel'),
                  ),
                  TextButton(
                    onPressed: () {
                      Navigator.of(context).pop();
                    },
                    child: Text('Add'),
                  ),
                ],
              );
            },
          );
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

In this code snippet, we are creating a stateful widget `HabitTrackingPage`, which holds a list of `Habit` objects. The `ListView.builder` displays each habit as a `ListTile`, allowing users to toggle the completion status using a `Checkbox`. The `floatingActionButton` triggers a dialog to add a new habit to the list when pressed.

### Integrating the Habit Tracking feature

To integrate the habit tracking feature into our MaterialApp, we can update the `HomePage` widget:

```dart
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Welcome to Habit Tracker!'),
            ElevatedButton(
              onPressed: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (context) => HabitTrackingPage(),
                  ),
                );
              },
              child: Text('Start Tracking Habits'),
            ),
          ],
        ),
      ),
    );
  }
}
```

Here, we added an elevated button that navigates to the `HabitTrackingPage` when pressed.

## Creating the Goal-Setting Feature

In addition to habit tracking, we can also add a goal-setting feature to help users set and track their personal goals. Let's create a new page called `GoalSettingPage`:

```dart
class GoalSettingPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Goal Setting'),
      ),
      body: Center(
        child: Text('Work in progress'),
      ),
    );
  }
}
```

In this simple implementation, we display a "Work in progress" message on the screen.

### Integrating the Goal-Setting feature

To integrate the goal-setting feature, we can update the `HomePage` widget again:

```dart
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Welcome to Habit Tracker!'),
            ElevatedButton(
              onPressed: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (context) => HabitTrackingPage(),
                  ),
                );
              },
              child: Text('Start Tracking Habits'),
            ),
            ElevatedButton(
              onPressed: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (context) => GoalSettingPage(),
                  ),
                );
              },
              child: Text('Set Goals'),
            ),
          ],
        ),
      ),
    );
  }
}
```

We added another elevated button that navigates to the `GoalSettingPage` when pressed.

## Conclusion

In this blog post, we learned how to create habit tracking and goal-setting features using the MaterialApp framework in Flutter. With MaterialApp, we can easily build consistent and responsive user interfaces. By implementing these features, users can track their habits and set goals to enhance their personal development and self-improvement.

[#Flutter](#flutter) [#MaterialApp](#materialapp)
---
layout: post
title: "Building a habit tracking app with alarm functionality in Flutter"
description: " "
date: 2023-09-18
tags: [AppDevelopment]
comments: true
share: true
---

In today's fast-paced world, it can be challenging to keep track of our daily habits and ensure we're staying on top of our goals. Thankfully, with the help of technology, we can build habit tracking apps to keep us accountable and motivated. In this article, we'll explore how to build a habit tracking app with alarm functionality using Flutter.

## Getting Started with Flutter

Before we dive into building our habit tracking app, make sure you have Flutter and Dart installed on your system. Flutter is an open-source UI framework for building natively compiled applications for mobile, web, and desktop platforms. Dart is the programming language used to write Flutter apps.

To create a new Flutter project, open your terminal or command prompt and run the following command:

```bash
flutter create habit_tracking_app
```

## Designing the App UI

Now that we have our Flutter project set up, let's design the user interface for our habit tracking app. We'll create a simple interface with a list of habits, each with a toggle button to mark them as completed and an alarm icon to set reminders.

First, navigate to the `lib` folder of your Flutter project and open the `main.dart` file. Replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(HabitTrackingApp());
}

class HabitTrackingApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Habit Tracking App',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: HabitListScreen(),
    );
  }
}

class HabitListScreen extends StatefulWidget {
  @override
  _HabitListScreenState createState() => _HabitListScreenState();
}

class _HabitListScreenState extends State<HabitListScreen> {
  List<String> habits = [
    'Exercise',
    'Read',
    'Meditate',
    'Drink water',
    'Write',
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Habit Tracking')),
      body: ListView.builder(
        itemCount: habits.length,
        itemBuilder: (context, index) {
          return ListTile(
            title: Text(habits[index]),
            trailing: Row(
              mainAxisSize: MainAxisSize.min,
              children: [
                Icon(Icons.alarm),
                SizedBox(width: 8),
                Icon(Icons.check_circle_outline),
              ],
            ),
          );
        },
      ),
    );
  }
}
```

Here, we create a basic Flutter app structure. The `HabitListScreen` is a `StatefulWidget` that holds a list of habits. Each habit is displayed as a `ListTile` with a title, an alarm icon, and a checkmark icon.

## Adding Alarm Functionality

Now that we have our UI in place, let's add alarm functionality to our habit tracking app. When the user taps on the alarm icon, we'll open a time picker to allow them to set a reminder for that habit.

To enable the time picker, update the `_HabitListScreenState` class as follows:

```dart
class _HabitListScreenState extends State<HabitListScreen> {
  List<String> habits = [
    'Exercise',
    'Read',
    'Meditate',
    'Drink water',
    'Write',
  ];
  Map<String, TimeOfDay> habitReminders = {};

  Future<void> _setReminder(String habit) async {
    final pickedTime = await showTimePicker(
      context: context,
      initialTime: TimeOfDay.now(),
    );
    
    if (pickedTime != null) {
      setState(() {
        habitReminders[habit] = pickedTime;
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Habit Tracking')),
      body: ListView.builder(
        itemCount: habits.length,
        itemBuilder: (context, index) {
          final habit = habits[index];
          final reminderTime = habitReminders[habit];
          
          return ListTile(
            title: Text(habit),
            trailing: Row(
              mainAxisSize: MainAxisSize.min,
              children: [
                IconButton(
                  icon: Icon(Icons.alarm),
                  onPressed: () => _setReminder(habit),
                ),
                SizedBox(width: 8),
                Icon(Icons.check_circle_outline),
              ],
            ),
            subtitle: reminderTime != null
                ? Text('Reminder set for ${reminderTime.format(context)}')
                : null,
          );
        },
      ),
    );
  }
}
```

In the updated code, we introduce the `habitReminders` map to store the reminder times for each habit. The `_setReminder` method displays a time picker when the alarm icon is pressed, allowing the user to set a reminder for the habit. The chosen time is then stored in the `habitReminders` map, and the UI is updated to display the reminder time below the habit title.

## Conclusion

Congratulations! You've successfully built a habit tracking app with alarm functionality using Flutter. This app allows users to track their habits, mark them as completed, and set reminders to stay on track. Feel free to explore and enhance the app further by adding features such as notifications, habit streaks, and data persistence.

Remember, developing a habit tracking app can be a valuable investment in building positive routines and achieving your goals. Start building your habit tracking app today!

\#Flutter #AppDevelopment
---
layout: post
title: "How to implement a habit reminder app using Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [appdevelopment]
comments: true
share: true
---

In today's busy world, it's easy to forget important habits or tasks we want to incorporate into our daily routine. To help solve this problem, we can implement a habit reminder app using Flutter Alarm Manager. This app will remind the user at specific times to perform their desired habits or tasks. Let's dive into the implementation steps:

## Step 1: Set up the Flutter Project

Start by setting up a new Flutter project or opening an existing one in your preferred development environment.

## Step 2: Install Dependencies

To use Flutter Alarm Manager, you need to add the following dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_alarm_manager: ^0.4.4
```

Then, run the command `flutter packages get` to install the package.

## Step 3: Define Habits

In the `lib` directory, create a new file named `habit.dart`. This file will contain the Habit class to represent a single habit. Define the class as follows:

```dart
class Habit {
  String name;
  TimeOfDay reminderTime;

  Habit({required this.name, required this.reminderTime});
}
```

The `Habit` class has two properties: `name` (the name of the habit) and `reminderTime` (the time when the habit reminder should be triggered).

## Step 4: Create the Habit Reminder Screen

In the `lib` directory, create a new file named `habit_reminder_screen.dart`. This file will contain the screen where the user can add, edit, and view their habits with reminder times.

It is beyond the scope of this tutorial to create the entire screen layout, but here is an example code snippet for the basic structure:

```dart
import 'package:flutter/material.dart';

class HabitReminderScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Habit Reminder'),
      ),
      body: Center(
        child: Column(
          children: [
            // Add habit widgets here
          ],
        ),
      ),
    );
  }
}
```

## Step 5: Implement Reminder Scheduler

In the `lib` directory, create a new file named `reminder_scheduler.dart`. This file will contain the logic to schedule reminders for each habit.

```dart
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
import 'package:your_project/habit.dart';

class ReminderScheduler {
  static final FlutterLocalNotificationsPlugin _flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();

  static Future<void> scheduleReminder(Habit habit) async {
    final id = habit.name.hashCode;

    final androidPlatformChannelSpecifics = AndroidNotificationDetails(
      'reminder_channel',
      'Reminder Channel',
      'Channel for habit reminders',
      importance: Importance.high,
      priority: Priority.high,
      styleInformation: DefaultStyleInformation(true, true),
    );

    final iosPlatformChannelSpecifics = IOSNotificationDetails();

    final platformChannelSpecifics = NotificationDetails(
      android: androidPlatformChannelSpecifics,
      iOS: iosPlatformChannelSpecifics,
    );

    final now = DateTime.now();
    final reminderDateTime = DateTime(now.year, now.month, now.day, habit.reminderTime.hour, habit.reminderTime.minute);

    await FlutterAlarmManager.schedule(
      id,
      reminderDateTime,
      platformChannelSpecifics,
      payload: habit.name,
      allowWhileIdle: true,
    );
  }

  static Future<void> cancelReminder(Habit habit) async {
    final id = habit.name.hashCode;
    await FlutterAlarmManager.cancel(id);
  }
}
```

In the `ReminderScheduler` class, we use Flutter Alarm Manager and Flutter Local Notifications to schedule reminders for each habit. The `scheduleReminder` method creates a unique identifier for each habit reminder, sets up platform-specific notification details, and schedules the reminder using Flutter Alarm Manager.

The `cancelReminder` method cancels a previously scheduled reminder using the habit's unique identifier.

## Step 6: Integrate Reminder Scheduler into the App

Go back to the `habit_reminder_screen.dart` file and modify the body of the `build` method to include the habits and reminder scheduling logic:

```dart
// Import Habit and ReminderScheduler classes
import 'package:your_project/habit.dart';
import 'package:your_project/reminder_scheduler.dart';

class HabitReminderScreen extends StatefulWidget {
  @override
  _HabitReminderScreenState createState() => _HabitReminderScreenState();
}

class _HabitReminderScreenState extends State<HabitReminderScreen> {
  List<Habit> habits = [];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Habit Reminder'),
      ),
      body: Center(
        child: Column(
          children: [
            for (var habit in habits)
              ListTile(
                title: Text(habit.name),
                subtitle: Text('Reminder Time: ${habit.reminderTime.format(context)}'),
                trailing: IconButton(
                  icon: Icon(Icons.delete),
                  onPressed: () => _deleteHabitReminder(habit),
                ),
              ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        child: Icon(Icons.add),
        onPressed: _addHabitReminder,
      ),
    );
  }

  void _addHabitReminder() async {
    final TimeOfDay? selectedTime = await showTimePicker(
      context: context,
      initialTime: TimeOfDay.now(),
    );

    if (selectedTime != null) {
      final habitName = 'Habit ${habits.length + 1}';
      final newHabit = Habit(name: habitName, reminderTime: selectedTime);

      setState(() {
        habits.add(newHabit);
      });

      await ReminderScheduler.scheduleReminder(newHabit);
    }
  }

  void _deleteHabitReminder(Habit habit) async {
    setState(() {
      habits.remove(habit);
    });

    await ReminderScheduler.cancelReminder(habit);
  }
}
```

In the code snippet above, we define the `_addHabitReminder` method to show a time picker to the user when they press the add button. Once they select a time, a new habit is created, added to the `habits` list, and scheduled using the `ReminderScheduler.scheduleReminder` method.

The `_deleteHabitReminder` method removes the habit from the `habits` list and cancels the scheduled reminder using `ReminderScheduler.cancelReminder`.

## Step 7: Run the App

You can now run your app using `flutter run` command and test the habit reminder functionality!

# Conclusion

In this tutorial, we walked through the steps to implement a habit reminder app using Flutter Alarm Manager. By following these steps, you can help users stay organized and on track with their daily habits. Remember to customize the app according to your specific needs and design preferences.

#flutter #appdevelopment
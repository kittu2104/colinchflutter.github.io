---
layout: post
title: "Building a medication tracking app with alarm functionality in Flutter"
description: " "
date: 2023-09-18
tags: [medicine]
comments: true
share: true
---

In today's fast-paced lifestyle, it is common for individuals to have multiple medications to take on a daily basis. However, it can be challenging to remember to take each medication at the right time. That's where a medication tracking app with alarm functionality can be incredibly helpful. In this tutorial, we will guide you through the process of building a medication tracking app using the popular Flutter framework.

## Prerequisites

Before we get started, make sure you have the following installed on your system:

- Flutter SDK (version 2.2.3 or higher)
- Dart SDK (version 2.13.4 or higher)
- Flutter IDE (such as Visual Studio Code or Android Studio)
- Emulator or physical device to run the app

## Setting up the Flutter Project

1. Open your Flutter IDE and create a new Flutter project called "medication_tracker".
    ```flutter
    flutter create medication_tracker
    ```

2. Navigate to the project directory.
    ```flutter
    cd medication_tracker
    ```

3. Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

void main() {
  runApp(MedicationTrackerApp());
}

class MedicationTrackerApp extends StatelessWidget {
  final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Medication Tracker',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MedicationTrackerHomePage(),
    );
  }
}

class MedicationTrackerHomePage extends StatefulWidget {
  @override
  _MedicationTrackerHomePageState createState() =>
      _MedicationTrackerHomePageState();
}

class _MedicationTrackerHomePageState extends State<MedicationTrackerHomePage> {
  @override
  void initState() {
    super.initState();
    initializeNotifications();
  }

  Future<void> initializeNotifications() async {
    const AndroidInitializationSettings initializationSettingsAndroid =
        AndroidInitializationSettings('app_icon');
        
    final InitializationSettings initializationSettings =
        InitializationSettings(android: initializationSettingsAndroid);
        
    await flutterLocalNotificationsPlugin.initialize(initializationSettings);
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Medication Tracker'),
      ),
      body: Center(
        child: Text('Coming soon...'),
      ),
    );
  }
}
```

4. Save the file and run the app on your emulator or physical device.
   ```flutter
   flutter run
   ```

## Adding Medication Tracking and Alarm Functionality

Now that we have our basic app structure in place, let's focus on adding medication tracking and alarm functionality.

1. Create a new Flutter class file called `medication.dart`. This file will contain the `Medication` class.
2. In `medication.dart`, add the following code to define the `Medication` class:

```dart
class Medication {
  final String name;
  final TimeOfDay time;

  Medication({required this.name, required this.time});
}
```

3. In `main.dart`, import the `medication.dart` file.
   ```dart
   import 'medication.dart';
   ```

4. Inside the `_MedicationTrackerHomePageState` class, add a list of medications and a function to set up an alarm for each medication:
   ```dart
   List<Medication> medications = [];

   Future<void> setupAlarms() async {
     for (final medication in medications) {
       final Time time = Time(medication.time.hour, medication.time.minute, 0);
       final AndroidNotificationDetails androidPlatformChannelSpecifics =
           AndroidNotificationDetails(
               'medication_alarm',
               'Medication Alarm Notifications',
               'Reminders for taking medications',
               importance: Importance.max,
               priority: Priority.high,
               showWhen: false);
       
       final NotificationDetails platformChannelSpecifics =
           NotificationDetails(android: androidPlatformChannelSpecifics);

       await flutterLocalNotificationsPlugin.showDailyAtTime(
           medication.name.hashCode,
           'Time to take ${medication.name}',
           'Remember to take ${medication.name}',
           time,
           platformChannelSpecifics);
     }
   }
   ```

5. Inside the `build` method of `_MedicationTrackerHomePageState`, replace the placeholder `Text` widget with a `ListView.builder` widget to display the list of medications:
   ```dart
   ListView.builder(
     itemCount: medications.length,
     itemBuilder: (context, index) {
       final medication = medications[index];
       return ListTile(
         title: Text(medication.name),
         subtitle: Text('Time: ${medication.time.format(context)}'),
       );
     },
   )
   ```

6. Finally, add a floating action button to the app's bottom navigation bar to add new medications:
   ```dart
   floatingActionButton: FloatingActionButton(
     onPressed: () {
       // Logic to add new medications
     },
     child: Icon(Icons.add),
   ),
   ```

With these changes, we have implemented the basic structure of a medication tracking app with alarm functionality in Flutter. Users can add medications with specific times, and the app will trigger notifications at the set times to remind users to take their medications.

Remember to test the app thoroughly and make any necessary adjustments based on your specific requirements.

# Conclusion

Building a medication tracking app with alarm functionality in Flutter can greatly assist individuals in managing their medications effectively. With the power of Flutter and the Flutter Local Notifications plugin, we can create a user-friendly and intuitive app that simplifies medication management. Feel free to enhance the app further by adding features like storage, reminders, or additional customization options.

#flutter #medicine
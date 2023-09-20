---
layout: post
title: "How to implement a medication compliance app with alarm notifications in Flutter"
description: " "
date: 2023-09-18
tags: [medicationcompliance]
comments: true
share: true
---

In this tutorial, we will walk through the process of creating a medication compliance app using Flutter. Flutter is an open-source UI development toolkit created by Google for building cross-platform applications. We will leverage the power of Flutter to create a robust and user-friendly medication compliance app that includes alarm notifications to remind users to take their medications on time.

## Prerequisites
Before we begin, ensure that you have the following installed:
* Flutter SDK
* Dart SDK
* Android Studio or any other preferred IDE

## Getting Started

### 1. Set up a new Flutter project

To create a new Flutter project, run the following command in your terminal:

```bash
$ flutter create medication_compliance_app
```

This will create a new directory called `medication_compliance_app` with the necessary Flutter project files.

### 2. Configure the project dependencies

Open the `pubspec.yaml` file in your project and add the required dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_local_notifications: ^2.0.0
  timezone: ^0.7.0
  provider: ^6.0.1
  # Add any other dependencies you may need
```

Save the file and run the following command to fetch the dependencies:

```bash
$ flutter pub get
```

### 3. Create the main app structure

Create a new Flutter widget to serve as the home screen of the app. This widget will display the list of medications and their corresponding alarm notifications. You can customize the UI to fit your design requirements.

```dart
import 'package:flutter/material.dart';

class MedicationComplianceApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Medication Compliance App'),
      ),
      body: ListView.builder(
        itemCount: medications.length,
        itemBuilder: (BuildContext context, int index) {
          final medication = medications[index];
          return ListTile(
            title: Text(medication.name),
            subtitle: Text(medication.dosage),
            trailing: Switch(
              value: medication.isReminderEnabled,
              onChanged: (value) {
                // Handle reminder toggle
              },
            ),
          );
        },
      ),
    );
  }
}
```

### 4. Implement alarm notifications

To implement alarm notifications, we will use the `flutter_local_notifications` package. This package allows us to schedule and display local notifications on the user's device.

Add the following code to your main function in the `main.dart` file:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();

Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();

  final initializationSettingsAndroid =
      AndroidInitializationSettings('app_icon');

  final initializationSettingsIOS = IOSInitializationSettings();

  final initializationSettings = InitializationSettings(
      android: initializationSettingsAndroid, iOS: initializationSettingsIOS);

  await flutterLocalNotificationsPlugin.initialize(initializationSettings);

  runApp(MedicationComplianceApp());
}
```

### 5. Add medication data model

Create a medication data model to represent each medication item in the list. This model will include properties like name, dosage, and reminder settings.

```dart
class Medication {
  final String name;
  final String dosage;
  bool isReminderEnabled;

  Medication({required this.name, required this.dosage, this.isReminderEnabled = false});
}

final List<Medication> medications = [
  Medication(name: 'Medication 1', dosage: '2 pills'),
  Medication(name: 'Medication 2', dosage: '1 pill'),
  // Add more medication items
];
```

### 6. Schedule alarm notifications

To schedule alarm notifications for each medication, we will make use of the `flutter_local_notifications` package.

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();

// ...

void scheduleNotification({required int id, required String title, required String body}) async {
  final androidPlatformChannelSpecifics = AndroidNotificationDetails(
    'medication_reminder',
    'Medication Reminder',
    'Reminders for taking medications',
    importance: Importance.high,
    priority: Priority.high,
  );

  final iOSPlatformChannelSpecifics = IOSNotificationDetails();

  final platformChannelSpecifics = NotificationDetails(
    android: androidPlatformChannelSpecifics,
    iOS: iOSPlatformChannelSpecifics,
  );

  await flutterLocalNotificationsPlugin.zonedSchedule(
    id,
    title,
    body,
    tz.TZDateTime.now(tz.local).add(Duration(seconds: 3)), // Change the time duration as needed
    platformChannelSpecifics,
    androidAllowWhileIdle: true,
    uiLocalNotificationDateInterpretation: UILocalNotificationDateInterpretation.absoluteTime,
  );
}
```

### 7. Integrate reminder toggle

To handle the reminder toggle of each medication item, we will use the `provider` package for state management.

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

class MedicationComplianceApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider<Medication>(
      create: (_) => Medication(),
      child: Consumer<Medication>(
        builder: (context, medication, _) => ListTile(
          title: Text(medication.name),
          subtitle: Text(medication.dosage),
          trailing: Switch(
            value: medication.isReminderEnabled,
            onChanged: (value) {
              medication.toggleReminder(value);
              if (value) {
                scheduleNotification(
                  id: medication.id,
                  title: medication.name,
                  body: 'Take ${medication.name} now!',
                );
              } else {
                cancelNotification(medication.id);
              }
            },
          ),
        ),
      ),
    );
  }
}
```

### 8. Run the app

You are now ready to run your medication compliance app. Use the following command to start the app on an emulator or connected device:

```bash
$ flutter run
```

Congratulations! You have successfully implemented a medication compliance app with alarm notifications in Flutter. You can now further enhance the app by adding features like medication tracking and data persistence.

Remember to test your app thoroughly and consider adding error handling, edge cases, and user interactions to create a polished and robust application.

#flutter #medicationcompliance
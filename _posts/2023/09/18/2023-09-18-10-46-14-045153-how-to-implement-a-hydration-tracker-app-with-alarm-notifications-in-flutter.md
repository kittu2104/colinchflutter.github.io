---
layout: post
title: "How to implement a hydration tracker app with alarm notifications in Flutter"
description: " "
date: 2023-09-18
tags: [hydrationTracker]
comments: true
share: true
---

In today's fast-paced lifestyle, it's important to stay hydrated throughout the day. To help you keep track of your water intake, we can create a hydration tracker app with alarm notifications using Flutter.

## Setting Up the Project

First, make sure you have Flutter installed on your machine. Follow the instructions on the Flutter website to get it set up.

Once Flutter is installed, create a new Flutter project using the following command:

```dart
flutter create hydration_tracker
```

Navigate into the project directory:

```dart
cd hydration_tracker
```

Open the project in your favorite code editor.

## Adding Dependencies

To implement alarm notifications, we need to add the following dependency to the `pubspec.yaml` file:

```yaml
dependencies:
  flutter_local_notifications: ^2.5.0
```

Save the file, and run the following command to fetch the dependencies:

```dart
flutter pub get
```

## Designing the App UI

For this example, let's create a simple UI with a text box to enter the amount of water consumed and a submit button to log it.

Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(HydrationTrackerApp());
}

class HydrationTrackerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Hydration Tracker',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: HydrationTrackerPage(),
    );
  }
}

class HydrationTrackerPage extends StatefulWidget {
  @override
  _HydrationTrackerPageState createState() => _HydrationTrackerPageState();
}

class _HydrationTrackerPageState extends State<HydrationTrackerPage> {
  int waterIntake;

  @override
  void initState() {
    super.initState();
    waterIntake = 0;
  }

  void addWaterIntake(int amount) {
    setState(() {
      waterIntake += amount;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Hydration Tracker'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Water Intake: $waterIntake ml',
              style: TextStyle(fontSize: 24),
            ),
            SizedBox(height: 20),
            RaisedButton(
              onPressed: () {
                // TODO: Implement the alarm notification logic
              },
              child: Text('Set Reminder'),
            ),
          ],
        ),
      ),
    );
  }
}
```

## Implementing Alarm Notifications

To implement alarm notifications, we'll use the `flutter_local_notifications` package we added earlier.

1. Import the necessary classes:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
```

2. Create an instance of `FlutterLocalNotificationsPlugin`:

```dart
FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();
```

3. Initialize the plugin in the `initState()` method of `_HydrationTrackerPageState`:

```dart
@override
void initState() {
  super.initState();
  
  var initializationSettingsAndroid =
      AndroidInitializationSettings('app_icon');
  var initializationSettingsIOS = IOSInitializationSettings();
  var initializationSettings = InitializationSettings(
      android: initializationSettingsAndroid, iOS: initializationSettingsIOS);

  flutterLocalNotificationsPlugin.initialize(initializationSettings);
}
```

4. Finally, add the code to trigger a local notification when the "Set Reminder" button is pressed:

```dart
RaisedButton(
  onPressed: () async {
    var time = Time(10, 0, 0); // Set the time for the notification

    var androidPlatformChannelSpecifics = AndroidNotificationDetails(
        'hydration_channel', 'Hydration', 'Reminders for water intake',
        importance: Importance.high, priority: Priority.high);
    var iOSPlatformChannelSpecifics =
        IOSNotificationDetails();
    var platformChannelSpecifics = NotificationDetails(
        android: androidPlatformChannelSpecifics,
        iOS: iOSPlatformChannelSpecifics);

    await flutterLocalNotificationsPlugin.showDailyAtTime(
        0,
        'Drink Water',
        'Stay hydrated! Drink water now.',
        time,
        platformChannelSpecifics);
  },
  child: Text('Set Reminder'),
),
```

Remember to replace the `app_icon` with the appropriate icon image file name.

## Testing the App

Now, run the app on a physical device or emulator using the following command:

```dart
flutter run
```

You should see the app with the UI as described earlier. Press the "Set Reminder" button, and you should receive a notification at the specified time reminding you to drink water.

## Conclusion

In this tutorial, we learned how to implement a hydration tracker app with alarm notifications in Flutter. By following these steps, you can create an app that helps you stay hydrated and receive timely reminders.

#flutter #hydrationTracker
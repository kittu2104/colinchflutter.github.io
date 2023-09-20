---
layout: post
title: "Building a bill payment reminder app with alarm functionality using Flutter"
description: " "
date: 2023-09-18
tags: [AppDevelopment]
comments: true
share: true
---

In this tutorial, we will be building a bill payment reminder app with alarm functionality using Flutter. Flutter is a cross-platform framework that allows you to build beautiful and fast native apps for iOS and Android from a single codebase.

## Requirements

To follow along with this tutorial, you will need:

- Flutter SDK installed on your machine.
- An IDE of your choice, such as Android Studio or Visual Studio Code.
- Basic knowledge of Flutter and Dart programming language.

## Getting Started

### 1. Set up a new Flutter project

To start, open your terminal and run the following command:

```sh
flutter create bill_payment_app
```

### 2. Design the app layout

Next, let's design the app layout. For simplicity, we will have a single screen with a list of bills and a button to add new bills.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(BillPaymentApp());
}

class BillPaymentApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Bill Payment App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: BillListScreen(),
    );
  }
}

class BillListScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Bill Payment Reminder'),
      ),
      body: ListView(
        children: [
          ListTile(
            title: Text('Electricity bill'),
            trailing: IconButton(
              icon: Icon(Icons.alarm),
              onPressed: () {
                // TODO: Implement alarm functionality
              },
            ),
          ),
          ListTile(
            title: Text('Internet bill'),
            trailing: IconButton(
              icon: Icon(Icons.alarm),
              onPressed: () {
                // TODO: Implement alarm functionality
              },
            ),
          ),
          // Add more bill items here
        ],
      ),
      floatingActionButton: FloatingActionButton(
        child: Icon(Icons.add),
        onPressed: () {
          // TODO: Implement add bill functionality
        },
      ),
    );
  }
}
```

### 3. Implement alarm functionality

Now, let's implement the alarm functionality for each bill item. When the alarm button is pressed, we will schedule a notification to remind the user of the bill payment.

To implement this, you will need to use the `flutter_local_notifications` package. Add the following dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_local_notifications: ^X.X.X
```

Replace `X.X.X` with the latest version of the package.

Then, import the necessary packages and add the code to schedule notifications in the `onPressed` callback of each bill item:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

// ...

class BillListScreen extends StatelessWidget {
  final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();

  Future<void> scheduleNotification() async {
    const AndroidInitializationSettings initializationSettingsAndroid =
        AndroidInitializationSettings('@mipmap/ic_launcher');
    final InitializationSettings initializationSettings =
        InitializationSettings(
      android: initializationSettingsAndroid,
    );
    await flutterLocalNotificationsPlugin.initialize(initializationSettings);
    const AndroidNotificationDetails androidPlatformChannelSpecifics =
        AndroidNotificationDetails(
      'bill_payment',
      'Bill Payment',
      'Reminder for bill payment',
      importance: Importance.max,
      priority: Priority.high,
      ticker: 'ticker',
    );
    const NotificationDetails platformChannelSpecifics =
        NotificationDetails(android: androidPlatformChannelSpecifics);
    await flutterLocalNotificationsPlugin.zonedSchedule(
      0,
      'Payment Reminder',
      'Remember to pay your bill.',
      DateTime.now().add(Duration(hours: 24)),
      platformChannelSpecifics,
      uiLocalNotificationDateInterpretation:
          UILocalNotificationDateInterpretation.absoluteTime,
      androidAllowWhileIdle: true,
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // ...
      body: ListView(
        children: [
          ListTile(
            title: Text('Electricity bill'),
            trailing: IconButton(
              icon: Icon(Icons.alarm),
              onPressed: () {scheduleNotification();},
            ),
          ),
          ListTile(
            title: Text('Internet bill'),
            trailing: IconButton(
              icon: Icon(Icons.alarm),
              onPressed: () {scheduleNotification();},
            ),
          ),
          // Add more bill items here
        ],
      ),
      // ...
    );
  }
}
```

### 4. Test the app

Now, run the app on an emulator or a device using the following command:

```sh
flutter run
```

You should see the bill items displayed with alarm buttons next to them. When you press the alarm button, a notification will be scheduled to remind you of the bill payment.

## Conclusion

In this tutorial, we built a bill payment reminder app with alarm functionality using Flutter. We learned how to create the app layout, implement the alarm functionality, and schedule notifications using the `flutter_local_notifications` package.

Feel free to customize the app further by adding features like deleting bills, editing bill details, or integrating with a backend database for persisting bill data.

Happy coding! 🚀

#Flutter #AppDevelopment
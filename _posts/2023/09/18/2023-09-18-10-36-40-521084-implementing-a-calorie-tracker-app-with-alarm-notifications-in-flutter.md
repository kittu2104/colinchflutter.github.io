---
layout: post
title: "Implementing a calorie tracker app with alarm notifications in Flutter"
description: " "
date: 2023-09-18
tags: [calorietracker]
comments: true
share: true
---

In this blog post, we'll explore how to build a calorie tracker app in Flutter that includes alarm notifications to remind users when to track their calorie intake. 

## Prerequisites
Make sure you have Flutter installed on your machine. If not, follow the official [Flutter installation guide](https://flutter.dev/docs/get-started/install) to set it up.

## Setting up the Project
1. Open your preferred IDE or code editor and create a new Flutter project:

    ```flutter
    flutter create calorie_tracker_app
    ```

2. Once the project is created, navigate to the project directory:

    ```flutter
    cd calorie_tracker_app
    ```

3. Open the `pubspec.yaml` file and add the necessary dependencies for the project:

    ```yaml
    dependencies:
      flutter:
        sdk: flutter
      cupertino_icons: ^1.0.2
      flutter_local_notifications: ^10.0.0
      shared_preferences: ^2.0.5
    ```

4. Run the following command to download the dependencies:

    ```flutter
    flutter pub get
    ```

## Designing the User Interface

1. Open the `lib/main.dart` file and replace the existing code with the following:

    ```dart
    import 'package:flutter/material.dart';
    
    void main() {
      runApp(CalorieTrackerApp());
    }
    
    class CalorieTrackerApp extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        return MaterialApp(
          title: 'Calorie Tracker',
          theme: ThemeData(
            primarySwatch: Colors.blue,
            visualDensity: VisualDensity.adaptivePlatformDensity,
          ),
          home: CalorieTrackerHome(),
        );
      }
    }
    
    class CalorieTrackerHome extends StatefulWidget {
      @override
      _CalorieTrackerHomeState createState() => _CalorieTrackerHomeState();
    }
    
    class _CalorieTrackerHomeState extends State<CalorieTrackerHome> {
      @override
      Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(
            title: Text('Calorie Tracker'),
          ),
          body: Center(
            child: Text(
              'Welcome to Calorie Tracker!',
              style: TextStyle(fontSize: 24),
            ),
          ),
        );
      }
    }
    ```

2. Save the changes and run the app using the following command:

    ```flutter
    flutter run
    ```

## Adding Alarm Notification Functionality

1. Open the `android/app/src/main/AndroidManifest.xml` file and add the following permission inside the `<manifest>` tag:

    ```xml
    <uses-permission android:name="android.permission.VIBRATE"/>
    ```

2. Open the `android/app/build.gradle` file and add the following dependency inside the `dependencies` block:

    ```gradle
    implementation 'com.github.bobbylight:bulb:0.2.12'
    ```

3. Create a new file named `notification_helper.dart` in the `lib` directory with the following code:

    ```dart
    import 'package:flutter_local_notifications/flutter_local_notifications.dart';
    
    class NotificationHelper {
      FlutterLocalNotificationsPlugin _flutterLocalNotificationsPlugin =
          FlutterLocalNotificationsPlugin();
    
      Future<void> initialize() async {
        const AndroidInitializationSettings initializationSettingsAndroid =
            AndroidInitializationSettings('@mipmap/ic_launcher');
    
        final InitializationSettings initializationSettings =
            InitializationSettings(android: initializationSettingsAndroid);
    
        await _flutterLocalNotificationsPlugin.initialize(initializationSettings);
      }
    
      Future<void> scheduleDailyNotification(
          Time notificationTime, int notificationId, String title, String body) async {
        final AndroidNotificationDetails androidPlatformChannelSpecifics =
            AndroidNotificationDetails(
          'calorie_tracker_app',
          'Calorie Tracker App',
          'Notification Channel for Calorie Tracker App',
          importance: Importance.max,
          priority: Priority.high,
        );
    
        final NotificationDetails platformChannelSpecifics =
            NotificationDetails(android: androidPlatformChannelSpecifics);
    
        await _flutterLocalNotificationsPlugin.showDailyAtTime(
          notificationId,
          title,
          body,
          notificationTime,
          platformChannelSpecifics,
        );
      }
    }
    ```

4. Open the `lib/main.dart` file and modify the `_CalorieTrackerHomeState` class as follows:

    ```dart
    import 'package:flutter/material.dart';
    import 'package:calorie_tracker_app/notification_helper.dart';
    import 'package:flutter_local_notifications/flutter_local_notifications.dart';
    
    void main() {
      runApp(CalorieTrackerApp());
    }
    
    class CalorieTrackerApp extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        return MaterialApp(
          title: 'Calorie Tracker',
          theme: ThemeData(
            primarySwatch: Colors.blue,
            visualDensity: VisualDensity.adaptivePlatformDensity,
          ),
          home: CalorieTrackerHome(),
        );
      }
    }
    
    class CalorieTrackerHome extends StatefulWidget {
      @override
      _CalorieTrackerHomeState createState() => _CalorieTrackerHomeState();
    }
    
    class _CalorieTrackerHomeState extends State<CalorieTrackerHome> {
      final NotificationHelper _notificationHelper = NotificationHelper();
    
      @override
      void initState() {
        super.initState();
        _initializeNotifications();
      }
    
      void _initializeNotifications() async {
        await _notificationHelper.initialize();
        await _scheduleDailyNotification();
      }
    
      Future<void> _scheduleDailyNotification() async {
        const String channelId = 'daily_notification';
        const String channelName = 'Daily Notification';
        const String channelDescription = 'Daily Notification Channel';
        const int notificationId = 0;
    
        await _notificationHelper.scheduleDailyNotification(
          Time(8, 0, 0),
          notificationId,
          'Calorie Tracker',
          'Don\'t forget to track your calorie intake today!',
        );
      }
    
      @override
      Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(
            title: Text('Calorie Tracker'),
          ),
          body: Center(
            child: Text(
              'Welcome to Calorie Tracker!',
              style: TextStyle(fontSize: 24),
            ),
          ),
        );
      }
    }
    ```

## Conclusion

In this blog post, we learned how to implement a calorie tracker app with alarm notifications in Flutter. We started by setting up the project and designing the basic user interface. Then, we added the alarm notification functionality using `flutter_local_notifications` plugin. With this app, users will receive daily reminders to track their calorie intake. Feel free to customize and extend this app according to your requirements.

#flutter #calorietracker #flutterapps #mobiledevelopment
---
layout: post
title: "Integrating Flutter Alarm Manager with Firebase Cloud Messaging"
description: " "
date: 2023-09-18
tags: [firebase]
comments: true
share: true
---

Flutter is a powerful framework that allows developers to build cross-platform mobile applications. One common feature in mobile apps is the ability to schedule and handle alarms or notifications. In this blog post, we will discuss how to integrate Flutter Alarm Manager with Firebase Cloud Messaging (FCM) to create and manage alarms in your Flutter app.

## Prerequisites
Before getting started, make sure you have the following prerequisites:

1. Flutter SDK installed on your machine.
2. A Firebase project set up with FCM enabled.

## Step 1: Add Dependencies
To get started, open your Flutter project and add the required dependencies to your `pubspec.yaml` file:

```dart
dependencies:
  flutter:
    sdk: flutter
  flutter_local_notifications: ^3.0.0
  firebase_messaging: ^9.0.0
  flutter_alarm_manager: ^0.5.0
```

Run `flutter pub get` to fetch and update the dependencies in your project.

## Step 2: Configure Firebase
Next, you need to configure Firebase in your Flutter app. Follow these steps to initialize Firebase:

1. Visit the Firebase console and create a new project.
2. Follow the instructions to add your Flutter app to the Firebase project.
3. Download the `google-services.json` file and place it inside the `android/app` directory of your Flutter project.

## Step 3: Initialize Flutter Alarm Manager
To use the Flutter Alarm Manager plugin, you need to initialize it in your app. Add the following code to your `main.dart` file:

```dart
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  
  await FlutterAlarmManager.initialize();

  runApp(MyApp());
}
```

## Step 4: Set Up Firebase Cloud Messaging
To receive FCM messages in your Flutter app, you need to set up Firebase Cloud Messaging. Add the following code to your `main.dart` file:

```dart
import 'package:firebase_messaging/firebase_messaging.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  await Firebase.initializeApp();
  await FirebaseMessaging.instance.setForegroundNotificationPresentationOptions(
      alert: true, badge: true, sound: true);

  // Add other Firebase messaging related code here

  runApp(MyApp());
}
```

## Step 5: Schedule and Handle Alarms
Now, let's schedule and handle alarms in your Flutter app. Add the following code to schedule a simple alarm:

```dart
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';

void scheduleAlarm() {
  FlutterAlarmManager.schedule(
    alarmDateTime: DateTime.now().add(Duration(seconds: 10)),
    alarmPayload: "alarm_payload",
    callback: myAlarmCallback,
    allowWhileIdle: true,
  );
}

void myAlarmCallback() {
  // Handle alarm logic here
}
```

In the above code, we schedule an alarm 10 seconds from the current time. When the alarm triggers, the `myAlarmCallback()` function will be called, allowing you to handle the alarm logic.

## Step 6: Receive FCM Notifications
To receive FCM notifications in your Flutter app, add the following code to your `main.dart` file:

```dart
import 'package:firebase_messaging/firebase_messaging.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  await Firebase.initializeApp();
  await FirebaseMessaging.instance.setForegroundNotificationPresentationOptions(
      alert: true, badge: true, sound: true);

  FirebaseMessaging.onMessage.listen((RemoteMessage message) {
    // Handle foreground FCM message here
  });

  FirebaseMessaging.onMessageOpenedApp.listen((RemoteMessage message) {
    // Handle background FCM message here
  });

  runApp(MyApp());
}
```

In the above code, we listen to the `onMessage` and `onMessageOpenedApp` streams to handle incoming FCM messages in the foreground and background, respectively.

## Conclusion
By integrating Flutter Alarm Manager with Firebase Cloud Messaging, you can schedule and manage alarms in your Flutter app efficiently. This combination allows you to schedule notifications and handle them effectively, enhancing the user experience of your app.

#flutter #firebase #flutteralarmmanager #firebasecloudmessaging
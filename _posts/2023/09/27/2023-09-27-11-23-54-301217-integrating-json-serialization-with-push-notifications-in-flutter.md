---
layout: post
title: "Integrating JSON serialization with push notifications in Flutter"
description: " "
date: 2023-09-27
tags: [pushnotifications]
comments: true
share: true
---

Push notifications are an essential feature in most mobile apps to keep users engaged and informed. Flutter, with its cross-platform capabilities, makes it easy to implement push notifications.

In this tutorial, we will cover how to integrate JSON serialization with push notifications in Flutter. JSON (JavaScript Object Notation) serialization is the process of converting structured data into a format that can be stored or transmitted.

## Prerequisites

Before starting, make sure you have the following:

1. Flutter SDK installed on your machine.
2. A Firebase project with push notifications enabled. You can follow the official Firebase documentation to set up Firebase Cloud Messaging (FCM) for your Flutter app.

## Step 1: Adding Dependencies

To handle push notifications and JSON serialization, we need to add two dependencies to our `pubspec.yaml` file.

```yaml
dependencies:
  firebase_messaging: ^X.X.X # Replace with the latest version
  json_annotation: ^X.X.X # Replace with the latest version
  json_serializable: ^X.X.X # Replace with the latest version
```

After adding the dependencies, run `flutter pub get` to download and update the project.

## Step 2: Setting Up Firebase Messaging

To receive push notifications, we need to set up Firebase Messaging in our Flutter app.

1. Follow the official Firebase documentation to configure Firebase Messaging for your Flutter app and retrieve the necessary files (e.g., `google-services.json` or `GoogleService-Info.plist`).

2. Add the Firebase Messaging initialization code to your `main.dart` file:

```dart
import 'package:firebase_messaging/firebase_messaging.dart';
  
void main() {
  WidgetsFlutterBinding.ensureInitialized();
  FirebaseMessaging.onBackgroundMessage(_firebaseMessagingBackgroundHandler);
  runApp(MyApp());
}

Future<void> _firebaseMessagingBackgroundHandler(RemoteMessage message) async {
  // Handle background messages here
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      // ...
    );
  }
}
```

The `_firebaseMessagingBackgroundHandler` function will handle messages received in the background. You can customize it to perform specific actions according to your app's needs.

## Step 3: Creating Models for JSON Serialization

To serialize and deserialize the data received from push notifications, we need to create data models that match the JSON structure.

1. Create a new file called `notification_model.dart` and define the following model:

```dart
import 'package:json_annotation/json_annotation.dart';

part 'notification_model.g.dart';

@JsonSerializable()
class NotificationModel {
  final String title;
  final String body;

  NotificationModel({required this.title, required this.body});

  factory NotificationModel.fromJson(Map<String, dynamic> json) =>
      _$NotificationModelFromJson(json);

  Map<String, dynamic> toJson() => _$NotificationModelToJson(this);
}
```

2. Run the command `flutter pub run build_runner build` to generate the serialization code. This will generate a file called `notification_model.g.dart`.

## Step 4: Handling Push Notifications

To handle push notifications and deserialize the received JSON data, we need to make changes to the `firebase_messaging` initialization code in `main.dart`.

```dart
import 'package:firebase_messaging/firebase_messaging.dart';
import 'notification_model.dart';
  
void main() {
  WidgetsFlutterBinding.ensureInitialized();
  FirebaseMessaging.onBackgroundMessage(_firebaseMessagingBackgroundHandler);
  FirebaseMessaging.onMessage.listen(_handleFirebaseMessage);
  runApp(MyApp());
}

void _handleFirebaseMessage(RemoteMessage message) {
  final notification = NotificationModel.fromJson(message.data);
  // Access properties of the notification model
  print(notification.title);
  print(notification.body);
}

// ...
```

The `_handleFirebaseMessage` function is triggered when a push notification is received. It deserializes the received JSON data into a `NotificationModel` object, allowing us to access the properties of the notification.

## Conclusion

In this tutorial, we learned how to integrate JSON serialization with push notifications in Flutter. We set up Firebase Messaging, created models for JSON serialization, and handled push notifications by deserializing the JSON data.

By using JSON serialization, we can easily work with structured data received from push notifications, making our Flutter app more powerful and flexible.

#flutter #pushnotifications
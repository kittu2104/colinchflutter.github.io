---
layout: post
title: "Implementing push notifications in Flutter SSR"
description: " "
date: 2023-09-21
tags: [flutter, pushnotifications]
comments: true
share: true
---

Push notifications are a powerful way to engage users and deliver timely information to your Flutter SSR app. Whether it's sending updates, reminders, or important announcements, implementing push notifications can greatly enhance the user experience. In this blog post, we will explore how to integrate push notifications in a Flutter Server Side Render (SSR) application.

## Prerequisites
Before we dive into the implementation, here are some prerequisites you need to have in place:
- A Firebase account with an active project.
- Knowledge of Flutter and Flutter SSR.

## Step 1: Set up Firebase Messaging
1. Navigate to the Firebase console and select your project.
2. Go to the "Project settings" and click on the "Cloud Messaging" tab.
3. Copy the **Server key** value, which we will use later in our Flutter SSR app.

## Step 2: Configure the Flutter SSR Project
1. Open your Flutter SSR project in your preferred code editor.
2. Add the `firebase_messaging` dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_messaging: ^8.0.0-dev.15
```

3. Run `flutter pub get` to fetch the dependencies.

## Step 3: Configure iOS (Optional)
If you plan to deploy your Flutter SSR app on iOS, follow these additional steps:

1. Navigate to the `AppDelegate.swift` file in the `ios/Runner` directory.
2. Add the following import statement at the top:

```swift
import Firebase
```

3. Insert the following code inside the `application(_:didFinishLaunchingWithOptions:)` function, before the `return` statement:

```swift
FirebaseApp.configure()
```

## Step 4: Configure Android
For Android, you need to add the Firebase configuration file:

1. Download the `google-services.json` file from Firebase console for your Android app.
2. Place the `google-services.json` file in the `android/app` directory of your Flutter SSR project.

## Step 5: Initialize Firebase Messaging
1. Create a new file named `push_notifications.dart` in your project's relevant directory.
2. Add the following code to initialize Firebase Messaging:

```dart
import 'package:firebase_messaging/firebase_messaging.dart';

class PushNotificationsManager {
  final FirebaseMessaging _firebaseMessaging = FirebaseMessaging.instance;

  Future<void> initialize() async {
    NotificationSettings settings = await _firebaseMessaging.requestPermission(
      alert: true,
      badge: true,
      sound: true,
    );

    if (settings.authorizationStatus == AuthorizationStatus.authorized) {
      print('Permission granted');
    } else {
      print('Permission denied');
    }
  }
}
```

## Step 6: Handle Incoming Messages
To handle incoming messages, modify the `initialize()` method as follows:

```dart
Future<void> initialize() async {
  FirebaseMessaging.onMessage.listen((RemoteMessage message) {
    print('Got a message whilst in the foreground!');
    print('Message data: ${message.data}');

    if (message.notification != null) {
      print('Message also contained a notification: ${message.notification}');
    }
  });
}
```

## Step 7: Displaying Notifications
To show notifications when the application is in the background, modify the `initialize()` method as follows:

```dart
Future<void> initialize() async {
  FirebaseMessaging.onBackgroundMessage(_firebaseMessagingBackgroundHandler);

  FirebaseMessaging.onMessage.listen((RemoteMessage message) {
    print('Got a message whilst in the foreground!');
    print('Message data: ${message.data}');

    if (message.notification != null) {
      print('Message also contained a notification: ${message.notification}');
    }
  });
}

Future<void> _firebaseMessagingBackgroundHandler(RemoteMessage message) async {
  print('Handling a background message: ${message.messageId}');
}
```

## Step 8: Testing Push Notifications
To test push notifications on your Flutter SSR app, you can use the `firebase_messaging` package's `firebase_messaging` command-line tool:

1. Have a connected physical device or an emulator.
2. Run the following command in your Flutter SSR project directory:

```bash
flutter pub run firebase_messaging serve
```

## Conclusion
Integrating push notifications in a Flutter SSR app can greatly enhance the user experience by delivering timely updates and notifications. By following the steps mentioned above, you can implement push notifications in your Flutter SSR project using Firebase Messaging. Explore further to customize the notifications and add specific actions based on your app's requirements.

#flutter #pushnotifications
---
layout: post
title: "Implementing push notifications in Flutter"
description: " "
date: 2023-10-13
tags: []
comments: true
share: true
---

Push notifications play a crucial role in keeping your users engaged and informed about updates and events in your mobile application. In this tutorial, we will explore how to implement push notifications in Flutter using Firebase Cloud Messaging (FCM) as the backend service.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Setting up Firebase Project](#setting-up-firebase-project)
- [Adding Dependency](#adding-dependency)
- [Configuring Firebase Cloud Messaging](#configuring-firebase-cloud-messaging)
- [Requesting User Permission](#requesting-user-permission)
- [Handling Push Notifications](#handling-push-notifications)
- [Sending Push Notifications](#sending-push-notifications)
- [Conclusion](#conclusion)

## Prerequisites

Before getting started, make sure you have the following:

- Flutter SDK installed on your machine
- A Firebase account

## Setting up Firebase Project

1. Go to the [Firebase Console](https://console.firebase.google.com/) and create a new project.

2. On the project dashboard, click on "Add app" and select the Flutter option.

3. Follow the instructions to register your app.

4. Download the `google-services.json` file and place it in the `android/app` directory of your Flutter project.

## Adding Dependency

Open your Flutter project's `pubspec.yaml` file and add the firebase_messaging dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_messaging: ^9.0.0-dev.2
```
Save the file and run `flutter pub get` to fetch the dependency.

## Configuring Firebase Cloud Messaging

1. In the Firebase Console, go to your project's settings and click on the "Cloud Messaging" tab.

2. Copy the **Server Key** and **Sender ID** values for later use.

3. In your Flutter project, create a new file named `firebase_messaging.dart` and add the following code:

```dart
import 'package:firebase_messaging/firebase_messaging.dart';

class FirebaseMessagingService {
  final FirebaseMessaging _firebaseMessaging = FirebaseMessaging.instance;
  
  Future<String?> getToken() async {
    return await _firebaseMessaging.getToken();
  }
}

final firebaseMessagingService = FirebaseMessagingService();
```

## Requesting User Permission

To receive push notifications, you need to request permission from the user. Add the following code to the main entry point of your Flutter app (e.g., `main.dart`).

```dart
import 'package:flutter/material.dart';
import 'package:firebase_messaging/firebase_messaging.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  
  FirebaseMessaging.onBackgroundMessage(_firebaseMessagingBackgroundHandler);
  FirebaseMessaging.onMessage.listen((message) {
    // Handle foreground notification
  });
  
  runApp(MyApp());
}
```

```dart
Future<void> _firebaseMessagingBackgroundHandler(RemoteMessage message) async {
  // Handle background notification
}
```

## Handling Push Notifications

When the app is in the foreground and receives a push notification, we process it in the `onMessage` callback function.

```dart
FirebaseMessaging.onMessage.listen((message) {
  // Handle foreground notification
});
```

When the app is in the background or terminated and receives a push notification, we process it in the `_firebaseMessagingBackgroundHandler` function.

```dart
Future<void> _firebaseMessagingBackgroundHandler(RemoteMessage message) async {
  // Handle background notification
}
```

## Sending Push Notifications

To send push notifications to your app, you can use the Firebase Cloud Messaging API or use the Firebase Console to send messages manually. You will need to use the **Server Key** and **Sender ID** values obtained in the previous steps.

## Conclusion

In this tutorial, we learned how to implement push notifications in Flutter using Firebase Cloud Messaging. We covered how to set up a Firebase project, add the necessary dependencies, handle user permission, process push notifications in the foreground and background, and send notifications to the app. With push notifications in place, you can now keep your users engaged and informed about updates and events in your Flutter app.

Feel free to explore more advanced features of Firebase Cloud Messaging, such as topic-based messaging and data payload handling, to enhance your push notification capabilities in Flutter.

Happy coding! 🚀

## References
- [Flutter Documentation](https://flutter.dev/)
- [Firebase Cloud Messaging Documentation](https://firebase.google.com/docs/cloud-messaging)
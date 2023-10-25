---
layout: post
title: "Handling push notifications with background services in Flutter"
description: " "
date: 2023-10-25
tags: []
comments: true
share: true
---

Push notifications are an essential feature for mobile apps as they allow us to engage with users even when the app is not actively being used. In Flutter, we can handle push notifications using background services, ensuring that users receive notifications even if they have closed the app. In this blog post, we will explore how to implement push notifications with background services in Flutter.

## Table of Contents
- [Introduction to Push Notifications](#introduction-to-push-notifications)
- [Setting up Firebase Cloud Messaging](#setting-up-firebase-cloud-messaging)
- [Implementing Background Services](#implementing-background-services)
- [Handling Push Notifications](#handling-push-notifications)
- [Conclusion](#conclusion)

## Introduction to Push Notifications

Push notifications are messages that can be sent to users even when they are not actively using an app. They are a great way to inform users about new updates, messages, or important events relevant to them. In Flutter, we can utilize push notifications by integrating with Firebase Cloud Messaging (FCM).

## Setting up Firebase Cloud Messaging

1. Create a new project on the [Firebase Console](https://console.firebase.google.com/).
2. Enable Firebase Cloud Messaging (FCM) for your project.
3. Add the Firebase SDK dependencies to your `pubspec.yaml` file.
   ```dart
   dependencies:
     firebase_messaging: ^7.0.3
     firebase_core: ^1.7.0
   ```
4. Run `flutter packages get` to install the dependencies.
5. Configure your Android and iOS project following the Firebase Console instructions.

## Implementing Background Services

To handle push notifications in the background, we need to implement background services. Flutter provides the `flutter_background_service` package, which allows us to execute Dart code in the background.

1. Add the `flutter_background_service` package to your `pubspec.yaml` file.
   ```dart
   dependencies:
     flutter_background_service: ^2.1.1
   ```
2. Run `flutter packages get` to install the package.
3. Implement your background service by extending the `BackgroundService` class.
   ```dart
   import 'package:flutter_background_service/flutter_background_service.dart';

   class MyBackgroundService extends BackgroundService {
     static Future<void> start() async {
       WidgetsFlutterBinding.ensureInitialized();
       await FlutterBackgroundService.initialize(MyBackgroundService.callback);
       FlutterBackgroundService().start();
     }

     static Future<void> callback() async {
       // Perform background tasks here
     }

     @override
     Future<void> onStart() {
       callback();
       return super.onStart();
     }
   }
   ```
4. Initialize and start the background service in the `main.dart` file.
   ```dart
   void main() {
     MyBackgroundService.start();
     runApp(MyApp());
   }
   ```

## Handling Push Notifications

To handle push notifications within the background service, we can use the `firebase_messaging` package.

1. Add the `firebase_messaging` package to your `pubspec.yaml` file.
   ```dart
   dependencies:
     firebase_messaging: ^10.2.1
   ```
2. Run `flutter packages get` to install the package.
3. Implement the necessary notification handling logic in the `MyBackgroundService` class.
   ```dart
   import 'package:firebase_messaging/firebase_messaging.dart';

   class MyBackgroundService extends BackgroundService {
     static FirebaseMessaging _firebaseMessaging = FirebaseMessaging.instance;

     static Future<void> callback() async {
       _firebaseMessaging.setAutoInitEnabled(true);
       _firebaseMessaging.getToken().then((token) {
         print('Firebase Token: $token');
       });

       FirebaseMessaging.onMessage.listen((RemoteMessage message) {
         // Handle the received notification message
       });

       FirebaseMessaging.onBackgroundMessage((RemoteMessage message) async {
         // Handle the received background notification message
         return Future<void>.value();
       });

       FirebaseMessaging.onMessageOpenedApp.listen((RemoteMessage message) {
         // Handle the notification message when the app is opened from a closed state
       });
     }

     // Rest of the background service implementation
   }
   ```

## Conclusion

By utilizing background services in Flutter, we can handle push notifications even when the app is not actively being used. This allows us to keep users engaged and informed about relevant updates and events. By following the steps outlined in this blog post, you can implement push notifications with background services in your Flutter app.

Remember to keep your background service lightweight and efficient to minimize the impact on device resources. Happy coding!

# References
- Official Flutter documentation on [Firebase Cloud Messaging](https://firebase.flutter.dev/docs/messaging/overview)
- Official Flutter package for [firebase_messaging](https://pub.dev/packages/firebase_messaging)
- Official Flutter package for [flutter_background_service](https://pub.dev/packages/flutter_background_service)
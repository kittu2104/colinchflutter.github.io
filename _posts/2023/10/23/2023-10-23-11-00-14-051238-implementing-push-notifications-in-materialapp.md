---
layout: post
title: "Implementing push notifications in MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Push notifications are a crucial feature in modern mobile applications, as they allow apps to reach out to users with important updates and notifications, even when the app isn't actively being used. In this blog post, we will explore how to implement push notifications in a MaterialApp - the most commonly used framework for building mobile apps using Flutter.

## Prerequisites

Before we begin, make sure you have the following prerequisites:

- Flutter SDK installed
- A code editor of your choice (e.g. Visual Studio Code, Android Studio)

## Setting up Firebase Cloud Messaging (FCM)

To implement push notifications in your MaterialApp, we will be using Firebase Cloud Messaging (FCM) - a widely used and reliable push notification service provided by Google. Follow the steps below to set up FCM for your Flutter project:

### Step 1: Create a Firebase project

1. Open the Firebase console at [https://console.firebase.google.com/](https://console.firebase.google.com/).
2. Click on "Add project" or select an existing project.
3. Follow the instructions to create a new Firebase project.

### Step 2: Configure the Android app

1. In the Firebase console, go to your project.
2. Click on "Add app" and select Android.
3. Follow the instructions to register your app with Firebase.
4. Download the `google-services.json` file and place it in the `android/app/` directory of your Flutter project.

### Step 3: Configure the iOS app

1. In the Firebase console, go to your project.
2. Click on "Add app" and select iOS.
3. Follow the instructions to register your app with Firebase.
4. Download the `GoogleService-Info.plist` file and add it to the root directory of your Flutter project.

### Step 4: Install Firebase packages

Open your Flutter project in your preferred code editor and add the necessary Firebase packages to your `pubspec.yaml` file:

```yaml
dependencies:
  firebase_core: ^1.5.0
  firebase_messaging: ^10.0.12
```

Save the file and run `flutter pub get` to fetch the dependencies.

## Implementing Push Notifications

Now that we have set up Firebase Cloud Messaging for our project, let's proceed with implementing push notifications in our MaterialApp.

### Step 1: Initialize Firebase Messaging

Open your `main.dart` file and import the necessary packages:

```dart
import 'package:firebase_core/firebase_core.dart';
import 'package:firebase_messaging/firebase_messaging.dart';
```

In the `main` function, add the following code to initialize Firebase:

```dart
Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  // ...
}
```

### Step 2: Configure Firebase Messaging

In your `main.dart` file, add the following code to configure Firebase Messaging:

```dart
FirebaseMessaging messaging = FirebaseMessaging.instance;

// Configuring Firebase Messaging
void configureFirebaseMessaging() {
  // Request permission for receiving notifications
  messaging.requestPermission();

  // Handling incoming messages when the app is in the foreground
  FirebaseMessaging.onMessage.listen((RemoteMessage message) {
    // Handle the received message
  });

  // Handling notification when the app is in the background or terminated
  FirebaseMessaging.onBackgroundMessage(handleBackgroundMessage);
}

// Handling background messages
Future<void> handleBackgroundMessage(RemoteMessage message) async {
  // Handle the received message
}
```

Call the `configureFirebaseMessaging()` function inside the `main` function to initialize Firebase Messaging.

### Step 3: Handling Notifications

To display notifications to the user, we will use Flutter's `flutter_local_notifications` package. Add the package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_local_notifications: ^10.4.0
```

Make sure to run `flutter pub get` after adding the package.

In your `main.dart` file, import the necessary packages:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
```

Below the initialization code, add the following code to configure the notification settings:

```dart
FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();

// Configuring notification settings
void configureNotificationSettings() async {
  const AndroidInitializationSettings initializationSettingsAndroid =
      AndroidInitializationSettings('app_icon');

  final InitializationSettings initializationSettings =
      InitializationSettings(
    android: initializationSettingsAndroid,
  );

  await flutterLocalNotificationsPlugin.initialize(
    initializationSettings,
    onSelectNotification: null,
  );
}
```

Call the `configureNotificationSettings()` function inside the `main` function to initialize the notification settings.

### Step 4: Displaying Notifications

To display a notification when a new message is received, add the following code inside the `onMessage` listener:

```dart
FirebaseMessaging.onMessage.listen((RemoteMessage message) async {
  // Handle the received message

  // Display the notification
  const AndroidNotificationDetails androidPlatformChannelSpecifics =
      AndroidNotificationDetails(
    'your_notification_channel_id',
    'your_notification_channel_name',
    'your_notification_channel_description',
    importance: Importance.max,
    priority: Priority.high,
  );
  const NotificationDetails platformChannelSpecifics =
      NotificationDetails(android: androidPlatformChannelSpecifics);

  await flutterLocalNotificationsPlugin.show(
    0,
    'Notification Title',
    'Notification Body',
    platformChannelSpecifics,
  );
});
```

### Step 5: Testing Push Notifications

To test push notifications in your MaterialApp, you can use the Firebase Cloud Messaging console to send a test message to your app.

1. In the Firebase console, go to your project.
2. Click on "Cloud Messaging" in the left-side menu.
3. Click on the "Compose notification" button.
4. Select your app from the "Send to" dropdown.
5. Enter the notification title and body.
6. Click on the "Send test message" button to send the notification.

## Conclusion

By following the steps outlined in this blog post, you should now be able to implement push notifications in your MaterialApp using Firebase Cloud Messaging. With this feature, you can keep your users informed and engaged with important updates and notifications, enhancing the overall user experience of your app.
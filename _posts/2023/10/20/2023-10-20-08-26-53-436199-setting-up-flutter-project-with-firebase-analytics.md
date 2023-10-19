---
layout: post
title: "Setting up Flutter project with Firebase Analytics"
description: " "
date: 2023-10-20
tags: [firebase]
comments: true
share: true
---

In this tutorial, we will walk you through the process of setting up a Flutter project with Firebase Analytics. Firebase Analytics is a powerful tool that allows you to track user interaction and gain insights into user behavior in your mobile app.

## Prerequisites
Before getting started, make sure you have the following:

1. Flutter SDK installed on your machine.
2. An existing Flutter project or create a new one.

Let's get started!

## Step 1: Set up Firebase Project

1. Go to the [Firebase Console](https://console.firebase.google.com/) and create a new project or select an existing one.
2. If you haven't already, click on "Add app" and select the Flutter platform.
3. Register your app with the package name of your Flutter project (e.g., com.example.myapp).
4. Follow the instructions to download the `google-services.json` file and place it inside the `android/app` directory.

## Step 2: Add Firebase Flutter SDK

1. Open your Flutter project in your preferred code editor.
2. Open the `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  firebase_core: ^1.0.0
  firebase_analytics: ^8.2.0
```

3. Run `flutter pub get` to fetch the dependencies.

## Step 3: Initialize Firebase Analytics

1. Open the `main.dart` file in the `lib` directory.
2. Add the following import statements at the top of the file:

```dart
import 'package:firebase_core/firebase_core.dart';
import 'package:firebase_analytics/firebase_analytics.dart';
```

3. Initialize Firebase in the `main` function before running the app:

```dart
Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}
```

## Step 4: Track Events with Firebase Analytics

1. To track an event, you can use the `FirebaseAnalytics` instance.
2. Import the following package:

```dart
import 'package:firebase_analytics/firebase_analytics.dart';
```

3. Inside a relevant function, instantiate `FirebaseAnalytics`:

```dart
FirebaseAnalytics analytics = FirebaseAnalytics();
```

4. To track an event, use the following code:

```dart
await analytics.logEvent(
  name: 'my_event',
  parameters: {'param1': 'value1', 'param2': 'value2'},
);
```

Replace `'my_event'` with the name of your event and provide any relevant parameters.

Congratulations! You have successfully set up Firebase Analytics in your Flutter project. You can now track user events and gain valuable insights into user behavior.

## Conclusion

In this tutorial, we learned how to set up a Flutter project with Firebase Analytics. We covered the steps to set up a Firebase project, add the necessary dependencies, initialize Firebase Analytics, and track events. Firebase Analytics provides valuable insights into user behavior, helping you make data-driven decisions for your mobile app.

Start integrating Firebase Analytics into your Flutter project today and gain a deeper understanding of your users.

**References:**
- [Firebase Documentation](https://firebase.google.com/docs)
- [Flutter Firebase Analytics Package](https://pub.dev/packages/firebase_analytics)

#flutter #firebase
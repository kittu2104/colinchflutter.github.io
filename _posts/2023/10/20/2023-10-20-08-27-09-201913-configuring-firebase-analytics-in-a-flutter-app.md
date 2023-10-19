---
layout: post
title: "Configuring Firebase Analytics in a Flutter app"
description: " "
date: 2023-10-20
tags: [firebase]
comments: true
share: true
---

Firebase Analytics is a powerful tool provided by Google that allows you to track user behavior and measure the performance of your app. In this blog post, we will guide you through the process of configuring Firebase Analytics in your Flutter app.

## Prerequisites

Before getting started, make sure you have the following:

1. A Flutter app already set up and running.
2. A Firebase project created and linked to your app. If you haven't set up Firebase in your Flutter app yet, you can refer to our previous blog post on how to [Integrate Firebase with Flutter](#link-to-previous-blog-post).

## Step 1: Add the Firebase Analytics package

To use Firebase Analytics in your Flutter app, you need to add the `firebase_analytics` package to your `pubspec.yaml` file. Open the file and add the following dependency:

```dart
dependencies:
  firebase_analytics: ^8.0.0
```

Save the file and run `flutter pub get` in your terminal to install the package.

## Step 2: Configure Firebase Analytics

1. Open the Firebase console in your web browser and navigate to your Firebase project.

2. In the left-hand menu, click on the "Analytics" tab.

3. Click on the "Get started" button under the "Data collection" section.

4. Follow the on-screen instructions to enable Firebase Analytics for your app.

5. Download the `google-services.json` file provided by Firebase and place it inside the `android/app` directory of your Flutter app.

6. Open the `AndroidManifest.xml` file located in `android/app/src/main` and add the following meta-data inside the `<application>` tag:

```xml
<meta-data
  android:name="com.google.firebase.analytics.FirebaseAnalyticsCollectionDeactivated"
  android:value="false" />
```

7. Save the file.

## Step 3: Initialize Firebase Analytics

In your Flutter app, navigate to the main entry file (`main.dart` by default) and import the `firebase_analytics` package:

```dart
import 'package:firebase_analytics/firebase_analytics.dart';
import 'package:firebase_analytics/observer.dart';
```

Initialize Firebase Analytics by adding the following code inside the `main` function:

```dart
void main() async {
  // Initialize Firebase Analytics
  await Firebase.initializeApp();
  
  // ...
  
  runApp(MyApp());
}
```

## Step 4: Track events

Firebase Analytics provides several methods to track events in your app. Here's an example of how to track a custom event:

```dart
FirebaseAnalytics analytics = FirebaseAnalytics();

void trackEvent(String eventName) {
  analytics.logEvent(
    name: eventName,
    parameters: {
      'timestamp': DateTime.now().toString(),
    },
  );
}
```

In this example, we create an instance of `FirebaseAnalytics` and use the `logEvent` method to log a custom event with a parameter called "timestamp".

## Step 5: Test Firebase Analytics

To test Firebase Analytics in your app, simply run your Flutter app on a physical device or an emulator. After a while, you should start seeing the analytics data appear in the Firebase console.

## Conclusion

Congratulations! You have successfully configured Firebase Analytics in your Flutter app. By tracking user behavior and analyzing the data collected, you can gain valuable insights to improve your app's performance and user experience.

If you have any further questions or need more assistance, refer to the [Firebase Analytics documentation](https://firebase.flutter.dev/docs/analytics/overview) or leave a comment below.

#flutter #firebase
---
layout: post
title: "Tracking user referrals and social sharing with Firebase Analytics in a Flutter app"
description: " "
date: 2023-10-20
tags: [FirebaseAnalytics]
comments: true
share: true
---

Firebase Analytics is a powerful tool provided by Google to help app developers track user interactions and analyze app usage. In this blog post, we will explore how to track user referrals and social sharing in a Flutter app using Firebase Analytics.

## Table of Contents
- [Introduction](#introduction)
- [Setting Up Firebase Analytics](#setting-up-firebase-analytics)
- [Tracking User Referrals](#tracking-user-referrals)
- [Tracking Social Sharing](#tracking-social-sharing)
- [Conclusion](#conclusion)

## Introduction
User referrals and social sharing play a crucial role in the success of any app. By tracking user referrals, you can understand which channels are driving the most app installations. Similarly, tracking social sharing will help you determine how users are engaging with your app and sharing it with others.

## Setting Up Firebase Analytics
Before we dive into tracking user referrals and social sharing, let's first set up Firebase Analytics in your Flutter app.

1. Create a new project in the Firebase console (https://console.firebase.google.com/) and add your Flutter app to the project.

2. Follow the Firebase setup instructions to add the Firebase SDK to your Flutter project.

3. Initialize Firebase Analytics in your app by adding the following code snippet to the `main.dart` file:

```dart
import 'package:firebase_analytics/firebase_analytics.dart';
import 'package:firebase_analytics/observer.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // Create an instance of Firebase Analytics
  final FirebaseAnalytics analytics = FirebaseAnalytics();

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My App',
      navigatorObservers: [
        FirebaseAnalyticsObserver(analytics: analytics),
      ],
      home: MyHomePage(),
    );
  }
}
```

With Firebase Analytics set up in your Flutter app, let's move on to tracking user referrals.

## Tracking User Referrals
Tracking user referrals allows you to identify the source or medium that led a user to install your app. This information can be valuable in understanding the effectiveness of different marketing campaigns or channels.

To track user referrals, you can use Firebase Dynamic Links, which automatically captures referral information and passes it to your app.

1. Create a dynamic link in the Firebase console by navigating to the Dynamic Links section and following the instructions.

2. Once you have created the link, you can share it via various channels such as email, social media, or SMS. When a user clicks on the link, it will redirect them to your app.

3. In your Flutter app, you can handle the dynamic link by adding the following code to your `main.dart` file:

```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  // Initialize Firebase
  await Firebase.initializeApp();
  // Handle the dynamic link
  FirebaseDynamicLinks.instance.onLink(
      onSuccess: (PendingDynamicLinkData dynamicLink) async {
    // Extract the referral information from the dynamic link
    final Uri deepLink = dynamicLink?.link;
    if (deepLink != null) {
      // Log the referral information to Firebase Analytics
      await FirebaseAnalytics.instance.logEvent(
        name: 'referral',
        parameters: <String, dynamic>{'link': deepLink.toString()},
      );
    }
  });

  runApp(MyApp());
}
```

With the above code, when a user installs your app by clicking on a dynamic link, the referral information will be logged to Firebase Analytics under the 'referral' event.

## Tracking Social Sharing
In addition to tracking user referrals, you can also track social sharing activities such as sharing content from your app to social media platforms. This will help you understand how users are promoting your app and the reach of your content.

To track social sharing, you can use the Firebase Analytics events to log the share actions performed by users.

1. Add the following code to your Flutter app wherever you have the logic for social sharing:

```dart
void shareContent() async {
  // Perform the social sharing
  // ...
  
  // Log the share event to Firebase Analytics
  await FirebaseAnalytics.instance.logEvent(
    name: 'share',
    parameters: <String, dynamic>{'content_id': '12345'},
  );
}
```

In the above code snippet, make sure to replace `'12345'` with the actual content ID you want to track.

2. Whenever a user performs a social sharing action, call the `shareContent` function to log the event to Firebase Analytics.

With the above implementation, you can track social sharing events and analyze which content is being shared the most.

## Conclusion
By tracking user referrals and social sharing in your Flutter app using Firebase Analytics, you can gain valuable insights into the effectiveness of your marketing campaigns and understand how users are engaging with your app.

Firebase Analytics provides a robust analytics framework that can help you make data-driven decisions and optimize your app's performance.

#hashtags #FirebaseAnalytics
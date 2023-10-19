---
layout: post
title: "Using Firebase Analytics to track screen views in a Flutter app"
description: " "
date: 2023-10-20
tags: []
comments: true
share: true
---

Firebase Analytics is a powerful tool that allows developers to track user interactions and gather valuable insights about their app. In Flutter, integrating Firebase Analytics is straightforward and can provide valuable information about user behavior. In this article, we will explore how to track screen views using Firebase Analytics in a Flutter app.

## Table of Contents
- [Setting up Firebase Analytics](#setting-up-firebase-analytics)
- [Tracking screen views](#tracking-screen-views)
- [Testing analytics events](#testing-analytics-events)
- [Conclusion](#conclusion)
- [References](#references)

## Setting up Firebase Analytics

Before we can start tracking screen views, we need to set up Firebase Analytics in our Flutter project. Follow these steps to get started:

1. Create a new Flutter project or open an existing one.

2. Add the `firebase_core` and `firebase_analytics` packages to your `pubspec.yaml` file:

   ```yaml
   dependencies:
     flutter:
       sdk: flutter
     firebase_core: ^1.5.0
     firebase_analytics: ^8.3.2
   ```

3. Run `flutter pub get` to fetch the new dependencies.

4. Register your app with Firebase by following the steps outlined in the official Firebase documentation.

5. Download the `google-services.json` file and place it in your Flutter project's `android/app` directory.

6. Add the following code to your `main.dart` file to initialize Firebase Analytics:

   ```dart
   import 'package:firebase_core/firebase_core.dart';
   import 'package:firebase_analytics/firebase_analytics.dart';

   void main() async {
     WidgetsFlutterBinding.ensureInitialized();
     await Firebase.initializeApp();
     runApp(MyApp());
   }

   class MyApp extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       FirebaseAnalytics().setCurrentScreen(
           screenName: 'Home',
       );
       return MaterialApp(
         title: 'Flutter Firebase Analytics',
         home: MyHomePage(),
       );
     }
   }
   ```

Now that Firebase Analytics is set up, we can proceed with tracking screen views.

## Tracking screen views

To track screen views, we need to call the `setCurrentScreen` method provided by Firebase Analytics. This method allows us to specify the current screen name, which will be reflected in the Firebase Analytics dashboard.

In Flutter, we can utilize the `WidgetsBindingObserver` mixin to track screen changes and call the `setCurrentScreen` method accordingly. Here's an example of how to implement this:

1. Create a new file called `analytics_service.dart` and add the following code:

   ```dart
   import 'package:firebase_analytics/firebase_analytics.dart';
   import 'package:flutter/widgets.dart';

   class AnalyticsService extends WidgetsBindingObserver {
     final FirebaseAnalytics _analytics = FirebaseAnalytics();

     static void init() {
       final AnalyticsService analyticsService = AnalyticsService();
       WidgetsBinding.instance!.addObserver(analyticsService);
     }

     @override
     void didPushRouteInformation(RouteInformation routeInformation) {
       setCurrentScreen(routeInformation.location!.toString());
     }

     void setCurrentScreen(String screenName) {
       _analytics.setCurrentScreen(screenName: screenName);
     }
   }
   ```

2. In your `main.dart` file, import the `analytics_service.dart` file and call the `AnalyticsService.init()` method before `runApp()`:

   ```dart
   void main() async {
     WidgetsFlutterBinding.ensureInitialized();
     Firebase.initializeApp();
     AnalyticsService.init();
     runApp(MyApp());
   }
   ```

By implementing the `setCurrentScreen` method in our `AnalyticsService` class and utilizing the `WidgetsBindingObserver` mixin, we can now track screen views.

## Testing analytics events

To test if our screen views are being tracked correctly, we can use the Firebase Analytics DebugView feature. To enable DebugView, follow these steps:

1. Open your app and navigate to the screen you want to test.

2. Open the Android Studio or Xcode console.

3. In your Flutter project's terminal, run the command `flutter run --observatory-port=5001`.

4. In the console, look for the Debug Console URL and open it in your browser.

5. Enable DebugView in the Firebase Analytics dashboard by clicking on the "DebugView" button.

6. Interact with your app and navigate to the screen you want to test. Each time the screen changes, you should see a corresponding log in the DebugView console.

## Conclusion

Firebase Analytics provides a powerful solution for tracking user behavior in a Flutter app. By integrating Firebase Analytics and implementing the `setCurrentScreen` method, developers can track screen views and gather valuable insights about user engagement.

In this article, we explored how to set up Firebase Analytics in a Flutter app and track screen views using the `setCurrentScreen` method. We also discussed how to test analytics events using the DebugView feature.

By leveraging Firebase Analytics, Flutter developers can make data-driven decisions and optimize their apps for a better user experience.

## References
- [Firebase Analytics Documentation](https://firebase.google.com/docs/analytics)
- [Flutter](https://flutter.dev/)
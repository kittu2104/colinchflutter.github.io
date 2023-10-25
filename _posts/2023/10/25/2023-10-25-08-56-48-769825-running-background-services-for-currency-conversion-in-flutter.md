---
layout: post
title: "Running background services for currency conversion in Flutter"
description: " "
date: 2023-10-25
tags: []
comments: true
share: true
---

In a mobile app, it's often necessary to perform tasks in the background, such as updating currency conversion rates. In Flutter, we can achieve this by using background services.

## What are background services?

Background services are components that run independently of the user interface and can perform tasks even when the app is not in the foreground. In the context of currency conversion, we can create a background service that periodically fetches the latest exchange rates and updates them in the app's database.

## Implementing background services in Flutter

To implement background services in Flutter, we can rely on platform-specific APIs. Let's explore the steps to achieve this on both Android and iOS.

### Android

For Android, we can use the `android_alarm_manager` package to set up periodic tasks. Here's how you can do it:

1. Add the `android_alarm_manager` package to your `pubspec.yaml` file.

   ```yaml
   dependencies:
     flutter:
       sdk: flutter
     android_alarm_manager: ^x.x.x
   ```

2. Follow the installation instructions provided by the `android_alarm_manager` package to set up alarms on Android.

3. Create a Dart function that represents the task you want to perform in the background, such as updating the currency rates.

   ```dart
   void updateCurrencyRates() {
     // Fetch and update the currency rates here
   }
   ```

4. Register the function as a background task in your Flutter app's `main.dart` file.

   ```dart
   void backgroundTask() => updateCurrencyRates();

   void main() async {
     // ...

     runApp(MyApp());

     // Register the background task
     await AndroidAlarmManager.initialize();
     await AndroidAlarmManager.periodic(
         const Duration(hours: 1), // Task interval
         0, // Unique identifier for the task
         backgroundTask,
         wakeup: true,
         rescheduleOnReboot: true,
     );
   }
   ```

### iOS

On iOS, background services are achieved using background fetch. Here's how you can implement it:

1. Open your Flutter project in Xcode by running `open ios/Runner.xcworkspace` in the terminal.

2. Enable the "Background Fetch" capability in your Xcode project's settings.

3. Update the `AppDelegate.swift` file to register the background fetch method.

   ```swift
   import UIKit
   import Flutter

   @UIApplicationMain
   @objc class AppDelegate: FlutterAppDelegate {
       override func application(
           _ application: UIApplication,
           didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
       ) -> Bool {
           GeneratedPluginRegistrant.register(with: self)

           // Register the background fetch method
           application.setMinimumBackgroundFetchInterval(
               UIApplication.backgroundFetchIntervalMinimum
           )

           return super.application(application, didFinishLaunchingWithOptions: launchOptions)
       }

       override func application(
           _ application: UIApplication,
           performFetchWithCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void
       ) {
           // Invoke the method to update currency rates
           let methodChannel = FlutterMethodChannel(name: "background_fetch", binaryMessenger: controller.binaryMessenger)
           methodChannel.invokeMethod("updateCurrencyRates", arguments: nil) { (result) in
               if let success = result as? Bool, success {
                   completionHandler(.newData)
               } else {
                   completionHandler(.noData)
               }
           }
       }
   }
   ```

4. Create a new Dart method in your Flutter app to handle the background fetch event and call the platform-specific method.

   ```dart
   MethodChannel _backgroundFetchChannel = MethodChannel('background_fetch');
   
   Future<void> updateCurrencyRates() async {
     await _backgroundFetchChannel.invokeMethod('updateCurrencyRates');
   }
   ```

Remember to handle the platform-specific method invocation appropriately in your native code.

## Conclusion

Running background services for currency conversion in Flutter enables your app to stay up-to-date with the latest exchange rates, even in the absence of user interaction. By using platform-specific APIs, such as `android_alarm_manager` for Android and background fetch for iOS, you can easily implement and manage these background tasks in Flutter.
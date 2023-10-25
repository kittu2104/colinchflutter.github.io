---
layout: post
title: "Running background services for text-to-speech conversion in Flutter"
description: " "
date: 2023-10-25
tags: []
comments: true
share: true
---

In Flutter, you might come across the need to convert text to speech, especially for tasks like reading out messages or providing audio feedback. However, performing text-to-speech conversion can be a resource-intensive operation, potentially affecting the UI responsiveness. To overcome this, you can run the text-to-speech conversion process in a background service.

## Using the Android AlarmManager

One way to achieve background services for text-to-speech conversion in Flutter is by utilizing the Android AlarmManager. This allows you to schedule periodic execution of a specific function even when the app is not in the foreground.

### Step 1: Add Required Dependencies

To get started, add the following dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_local_notifications: ^9.0.0
  android_alarm_manager: ^2.0.0
```

### Step 2: Configure Android AlarmManager

Configure the `AndroidManifest.xml` file to enable the use of Android AlarmManager. Add the following permissions and receivers inside the `<application>` tag:

```xml
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>

<receiver
    android:name="com.dexterous.flutterlocalnotifications.ScheduledNotificationReceiver"
    android:enabled="true" />  
```

### Step 3: Initialize Platform-Specific Code

To interact with native code, create a new file `background_service.dart` and add the following code:

```dart
import 'package:flutter/services.dart';
import 'package:android_alarm_manager/android_alarm_manager.dart';

class BackgroundService {
  static void textToSpeech() {
    // Perform text-to-speech conversion logic here
  }

  static void initialize() async {
    const androidPlatformChannelSpecifics =
        AndroidInitializationSettings('app_icon');
    const initializationSettings =
        InitializationSettings(android: androidPlatformChannelSpecifics);

    // Initialize FlutterLocalNotificationsPlugin
    await flutterLocalNotificationsPlugin.initialize(
      initializationSettings,
      onSelectNotification: (String? payload) async {
        // Handle notification click event
      },
    );

    await AndroidAlarmManager.initialize();
    await AndroidAlarmManager.periodic(
      const Duration(minutes: 1),
      0,
      textToSpeech,
      wakeup: true,
      rescheduleOnReboot: true,
    );
  }
}
```

This code initializes the FlutterLocalNotificationsPlugin and schedules the text-to-speech conversion to occur periodically every minute. You can adjust the duration as per your requirements.

### Step 4: Call BackgroundService Initialization

In your `main.dart` file, call the `BackgroundService.initialize()` method in the `void main()` function:

```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await BackgroundService.initialize();
  runApp(MyApp());
}
```

Now, whenever you launch your Flutter app, the text-to-speech conversion process will run in the background at the specified intervals, even when the app is not in the foreground.

## Conclusion

By utilizing the Android AlarmManager and running the text-to-speech conversion logic in a background service, you can ensure that the process continues even when the app is not actively being used. This approach helps improve the overall performance and responsiveness of your Flutter app.

# References
- [Flutter Local Notifications Package](https://pub.dev/packages/flutter_local_notifications)
- [Android AlarmManager Plugin](https://pub.dev/packages/android_alarm_manager)
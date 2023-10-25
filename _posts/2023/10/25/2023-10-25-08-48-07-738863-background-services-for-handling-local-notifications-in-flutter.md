---
layout: post
title: "Background services for handling local notifications in Flutter"
description: " "
date: 2023-10-25
tags: [notifications]
comments: true
share: true
---

In a Flutter app, you may need to schedule and display local notifications even when the app is not running or in the background. To achieve this, you can utilize background services to handle the scheduling and displaying of local notifications.

### Why Use Background Services?

Background services allow your app to perform tasks in the background, such as handling local notifications, even when the app is not active or in the foreground. This ensures that users receive notifications at the appropriate times, enhancing the user experience and keeping them engaged with your app.

### Implementing Background Services in Flutter

To implement background services for handling local notifications in Flutter, you can use the [flutter_local_notifications](https://pub.dev/packages/flutter_local_notifications) package. This package provides a simple and efficient way to schedule and display local notifications.

1. Start by adding the `flutter_local_notifications` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_local_notifications: ^x.x.x
```

Replace `^x.x.x` with the latest version of the package.

2. Import the necessary files in your Dart file:

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
```

3. Initialize the `flutter_local_notifications` package:

```dart
FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();
```

4. Set up the required notification initialization settings:

```dart
final initializationSettings = InitializationSettings(
  android: AndroidInitializationSettings('app_icon'),
  iOS: IOSInitializationSettings(
    onDidReceiveLocalNotification: (id, title, body, payload) =>
        YourNotificationHandler.onDidReceiveLocalNotification(
            id, title, body, payload),
  ),
);
```

Replace `'app_icon'` with the name of your app icon file.

5. Initialize the notifications:

```dart
await flutterLocalNotificationsPlugin.initialize(initializationSettings,
    onSelectNotification: (payload) =>
        YourNotificationHandler.onSelectNotification(payload));
```

6. Schedule and display a local notification:

```dart
var androidPlatformChannelSpecifics = AndroidNotificationDetails(
    'your_channel_id', 'your_channel_name', 'your_channel_description',
    importance: Importance.max, priority: Priority.high, showWhen: false);
var iOSPlatformChannelSpecifics = IOSNotificationDetails();
var platformChannelSpecifics = NotificationDetails(
    android: androidPlatformChannelSpecifics,
    iOS: iOSPlatformChannelSpecifics);
await flutterLocalNotificationsPlugin.show(
    0, 'Notification Title', 'Notification Body', platformChannelSpecifics,
    payload: 'notification_payload');
```

Replace `'your_channel_id'`, `'your_channel_name'`, and `'your_channel_description'` with your preferred channel details.

7. Handle notification selection:

```dart
class YourNotificationHandler {
  static Future<dynamic> onDidReceiveLocalNotification(
      int id, String title, String body, String payload) async {
    // Handle notification received while the app is in the foreground
  }

  static Future<dynamic> onSelectNotification(String payload) async {
    // Handle notification selection
  }
}
```

8. Make sure to properly configure background services. For Android, add the following to your `AndroidManifest.xml` file:

```xml
<application
    android:name="io.flutter.app.FlutterApplication"
    ...
    <service
        android:name="com.dexterous.flutterlocalnotifications.FlutterLocalNotificationsService"
        android:exported="false" />
    <receiver
        android:name="com.dexterous.flutterlocalnotifications.ScheduledNotificationBootReceiver"
        android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED"></action>
        </intent-filter>
    </receiver>
    <receiver
        android:name="com.dexterous.flutterlocalnotifications.ScheduledNotificationReceiver"
        android:exported="false" />
    ...
</application>
```

For iOS, no additional configuration is required.

### Conclusion

Implementing background services for handling local notifications in Flutter is essential for ensuring that your app can schedule and display notifications even when it is not running or in the background. By using the `flutter_local_notifications` package, you can easily integrate this functionality into your Flutter app and enhance the overall user experience.

[#flutter](https://flutter.dev/) [#notifications](https://flutter.dev/docs/development/ui/notifications)
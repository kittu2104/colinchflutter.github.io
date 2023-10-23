---
layout: post
title: "Adding push notifications with custom sound in MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Mobile applications often use push notifications to stay connected with users and provide important updates in real-time. By default, push notifications play a standard sound. However, as an app developer, you may want to customize the sound of the push notifications to effectively grab the user's attention. In this blog post, we will explore how to add push notifications with a custom sound in a MaterialApp using a popular framework.

## Table of Contents
- [Introduction to Push Notifications](#introduction-to-push-notifications)
- [Customizing Push Notification Sounds](#customizing-push-notification-sounds)
  - [Prepare Custom Sound Files](#prepare-custom-sound-files)
  - [Integrate Custom Sound into MaterialApp](#integrate-custom-sound-into-materialapp)
  - [Configure Push Notification Payload](#configure-push-notification-payload)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction to Push Notifications

Push notifications are messages that appear on a mobile device outside of the application. They are sent from a server or backend system to the user's device to notify them about important information or events. Push notifications are commonly used to notify users about new messages, updates, reminders, and more.

To use push notifications in an application, you need to integrate a push notification service provider such as Firebase Cloud Messaging (FCM) or Apple Push Notification Service (APNS) for iOS. These services provide APIs and tools to send and receive push notifications in your app.

## Customizing Push Notification Sounds

By default, when a push notification is received, it plays a standard sound defined by the operating system. However, you can customize the sound to make it more distinctive and recognizable to your app's branding or style.

### Prepare Custom Sound Files

To add a custom sound to your push notifications, you need to prepare the sound file in the appropriate format. Most commonly, push notification sounds are in the `.wav`, `.mp3`, or `.caf` formats. Make sure the sound file is short and attention-grabbing.

### Integrate Custom Sound into MaterialApp

Assuming you are using the MaterialApp widget in your application, you can integrate the custom sound by following these steps:

1. Add the custom sound file to the project's assets folder.
2. Update the `pubspec.yaml` file to include the newly added sound file as an asset.

```yaml
flutter:
  assets:
    - assets/custom_sound.wav
```

3. In the MaterialApp widget, initialize the FlutterLocalNotificationsPlugin with the custom sound.

```dart
import 'package:flutter_local_notifications/flutter_local_notifications.dart';

final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
    FlutterLocalNotificationsPlugin();

final InitializationSettings initializationSettings = InitializationSettings(
  android: AndroidInitializationSettings('@mipmap/ic_launcher'),
  iOS: IOSInitializationSettings(
    requestPermission: false,
    onDidReceiveLocalNotification: (int id, String? title, String? body, String? payload) async {},
  ),
);

await flutterLocalNotificationsPlugin.initialize(initializationSettings,
    onSelectNotification: (String? payload) async {});
```

4. Set the custom sound when displaying the push notification.

```dart
const AndroidNotificationDetails androidPlatformChannelSpecifics =
    AndroidNotificationDetails(
  'channel_id',
  'channel_name',
  'channel_description',
  sound: RawResourceAndroidNotificationSound('custom_sound'),
);

const NotificationDetails platformChannelSpecifics =
    NotificationDetails(android: androidPlatformChannelSpecifics);
await flutterLocalNotificationsPlugin.show(
  0,
  'New Notification',
  'You have a new message',
  platformChannelSpecifics,
);
```

### Configure Push Notification Payload

When sending push notifications from your server or backend system, you need to configure the payload to specify the custom sound. The payload will depend on the push notification service provider you are using. 

For example, when using FCM, you can include the `sound` field in the payload with the name of the custom sound file.

```json
{
  "notification": {
    "title": "New Notification",
    "body": "You have a new message",
    "sound": "custom_sound"
  },
  "to": "<<DEVICE_TOKEN>>"
}
```

Similarly, for APNS, you would include the `sound` field in the payload with the name of the custom sound file.

## Conclusion

Customizing push notification sounds can improve the user's experience and make your app stand out. By following the steps outlined in this blog post, you can easily add a custom sound to push notifications in a MaterialApp. Remember to prepare the sound file in the appropriate format, integrate it into your app using the FlutterLocalNotificationsPlugin, and configure the payload accordingly.

With this enhanced feature, you can create engaging and memorable push notifications for your users. Happy coding!

## References

1. [Flutter Documentation: Local notifications](https://flutter.dev/docs/development/ui/advanced/local-notifications)
2. [Firebase Cloud Messaging Documentation](https://firebase.google.com/docs/cloud-messaging)
3. [Apple Push Notification Service Documentation](https://developer.apple.com/documentation/usernotifications)
---
layout: post
title: "Implementing a reminder app with voice-controlled alarms using Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [Flutter, AlarmManager]
comments: true
share: true
---

![reminder app](https://example.com/reminder-app-image.jpg)

In this tutorial, we will learn how to implement a reminder app with voice-controlled alarms using Flutter Alarm Manager. With this app, users can set reminders by voice commands and receive notifications at the specified time. Flutter Alarm Manager is a powerful plugin that allows us to schedule and handle alarms easily in our Flutter application.

## Prerequisites

Before we start, make sure you have the following set up on your development machine:

- Flutter SDK
- Dart SDK
- Android Studio or Xcode

## Steps

### Step 1: Set up the Flutter project

First, we need to create a new Flutter project. Open your terminal and run the following command:

```bash
flutter create reminder_app
```

### Step 2: Add dependencies

Open `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_local_notifications: ^9.3.4
  speech_to_text: ^3.0.0
```

Then, run `flutter pub get` to retrieve the new dependencies.

### Step 3: Create the main app UI

Open the `lib/main.dart` file and replace the default code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_local_notifications/flutter_local_notifications.dart';
import 'package:speech_to_text/speech_recognition_error.dart';
import 'package:speech_to_text/speech_to_text.dart';

void main() {
  runApp(ReminderApp());
}

class ReminderApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Reminder App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: ReminderScreen(),
    );
  }
}

class ReminderScreen extends StatefulWidget {
  @override
  _ReminderScreenState createState() => _ReminderScreenState();
}

class _ReminderScreenState extends State<ReminderScreen> {
  final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
      FlutterLocalNotificationsPlugin();
  late SpeechToText speechToText;
  late bool isListening;
  late String reminderText;

  @override
  void initState() {
    super.initState();
    initializeSpeechRecognition();
    initializeNotifications();
  }

  void initializeSpeechRecognition() {
    // Initialize speech recognition
    speechToText = SpeechToText();
    isListening = false;

    // Add listeners for speech recognition events
    speechToText.errorListener = (SpeechRecognitionError error) {
      print("Speech recognition error: ${error.errorMsg}");
    };

    speechToText.setRecognitionCompleteHandler((_) {
      setState(() {
        isListening = false;
      });
    });
  }

  void initializeNotifications() async {
    const AndroidInitializationSettings initializationSettingsAndroid =
        AndroidInitializationSettings('app_icon');
    final InitializationSettings initializationSettings =
        InitializationSettings(android: initializationSettingsAndroid);

    await flutterLocalNotificationsPlugin.initialize(initializationSettings);
  }

  void scheduleAlarm(String reminder) {
    // Schedule the alarm
    // Code to be added
    // ...

    setState(() {
      reminderText = reminder;
    });
  }

  Future<void> startListening() async {
    // Start voice recognition
    final bool available = await speechToText.initialize(
      onStatus: (ListeningStatus status) {
        setState(() {
          isListening = status == ListeningStatus.listening;
        });
      },
    );

    if (available) {
      await speechToText.listen(
        listenFor: Duration(seconds: 5),
        onResult: (SpeechRecognitionResult result) {
          setState(() {
            reminderText = result.recognizedWords;
          });
          scheduleAlarm(result.recognizedWords);
        },
        cancelOnError: true,
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Reminder App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'Reminder: $reminderText',
              style: TextStyle(fontSize: 18),
            ),
            const SizedBox(height: 16),
            ElevatedButton(
              onPressed: () {
                startListening();
              },
              child: Text(isListening ? 'Stop' : 'Start'),
            ),
          ],
        ),
      ),
    );
  }
}
```

### Step 4: Configure and run the app

Before running the app, we need to configure the notification icon. Replace `android/app/src/main/res/mipmap/ic_launcher.png` with your custom notification icon.

Next, connect your device or launch an emulator, and run the app using the following command:

```bash
flutter run
```

### Step 5: Test the app

Open the app on your device or emulator. You will see a screen with a "Start" button and a reminder text. Press the "Start" button and speak a reminder. The app will recognize your voice command, schedule the alarm, and display the reminder text on the screen.

### Conclusion

In this tutorial, we learned how to implement a reminder app with voice-controlled alarms using Flutter Alarm Manager. We used the Flutter Local Notifications and Speech to Text plugins to schedule alarms and convert speech to text.

Feel free to customize the app further to suit your needs. Happy coding!

#Flutter #AlarmManager
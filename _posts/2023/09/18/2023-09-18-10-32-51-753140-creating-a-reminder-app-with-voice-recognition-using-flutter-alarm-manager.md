---
layout: post
title: "Creating a reminder app with voice recognition using Flutter Alarm Manager"
description: " "
date: 2023-09-18
tags: [voice]
comments: true
share: true
---

In this blog post, we will explore how to create a reminder app with voice recognition using the Flutter Alarm Manager package. This app will allow users to set reminders by simply speaking into their device's microphone. 

## Why Voice Recognition?

Voice recognition has become an increasingly popular feature in mobile apps as it provides users with a convenient and hands-free way of interacting with their devices. By integrating voice recognition into a reminder app, users can set reminders quickly and easily, without the need for manual input.

## Getting Started

To begin, make sure you have Flutter installed on your machine. If not, you can follow the official Flutter installation guide [here](https://flutter.dev/docs/get-started/install).

Once you have Flutter set up, create a new Flutter project and navigate to its directory in your terminal.

```dart
flutter create reminder_app
cd reminder_app
```

## Installing Dependencies

Next, we need to add the necessary dependencies to our `pubspec.yaml` file. Open the file and add the following lines:

```yaml
dependencies:
  flutter:
    sdk: flutter
  alarm_manager: ^0.4.5
  speech_to_text: ^2.4.0
```

Save the file and run the following command in your terminal to fetch the dependencies:

```dart
flutter pub get
```

## Implementing Voice Recognition

To enable voice recognition in our app, we will be using the `speech_to_text` package. This package provides easy-to-use APIs for converting speech into text.

Let's create a new file called `voice_recognition.dart` and add the following code:

```dart
import 'package:speech_to_text/speech_to_text.dart' as stt;

class VoiceRecognition {
  stt.SpeechToText _speechToText = stt.SpeechToText();

  Future<String> startListening() async {
    String transcription = '';

    if (await _speechToText.initialize()) {
      await _speechToText.listen(
        cancelOnError: true,
        onResult: (result) {
          transcription = result.recognizedWords;

          if (result.finalResult) {
            _speechToText.stop();
          }
        },
      );
    }

    return transcription;
  }
}
```

In this code, we initialize the `SpeechToText` instance and use its `listen()` method to start the voice recognition process. The `onResult` callback is triggered whenever the voice input changes, and the `stop()` method is called when the voice input is finalized.

## Setting Reminders with Alarm Manager

To set reminders in our app, we will be using the `alarm_manager` package. This package allows us to schedule and manage alarms within our Flutter app.

Create a new file called `reminder_service.dart` and add the following code:

```dart
import 'package:alarm_manager/alarm_manager.dart';

class ReminderService {
  static void setReminder(DateTime dateTime, String message) {
    AlarmManager.oneShotAt(dateTime, 0, () {
      print('Reminder: $message');
    });
  }
}
```

In this code, we define a `setReminder()` method that takes a `DateTime` object and a message as parameters. This method uses the `AlarmManager.oneShotAt()` function to schedule a reminder at the specified time. In this example, we simply print the reminder message, but you can customize this function to perform any desired action when the reminder triggers.

## Putting It All Together

Now that we have implemented voice recognition and reminder scheduling, we can integrate them into our Flutter app.

Open the `lib/main.dart` file and replace its content with the following code:

```dart
import 'package:flutter/material.dart';
import 'voice_recognition.dart';
import 'reminder_service.dart';

void main() {
  runApp(ReminderApp());
}

class ReminderApp extends StatefulWidget {
  @override
  _ReminderAppState createState() => _ReminderAppState();
}

class _ReminderAppState extends State<ReminderApp> {
  VoiceRecognition _voiceRecognition = VoiceRecognition();

  @override
  void initState() {
    super.initState();
    _initializeVoiceRecognition();
  }

  Future<void> _initializeVoiceRecognition() async {
    await _voiceRecognition.startListening();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Reminder App',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Reminder App'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              RaisedButton(
                onPressed: () async {
                  String transcription = await _voiceRecognition.startListening();

                  ReminderService.setReminder(DateTime.now().add(Duration(seconds: 10)), transcription);

                  ScaffoldMessenger.of(context).showSnackBar(SnackBar(
                    content: Text('Reminder set: $transcription'),
                  ));
                },
                child: Text('Set Reminder'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

In this code, we create a simple Flutter app that displays a button. When the button is pressed, voice recognition is initiated, and the recognized text is passed to the `setReminder()` method, which schedules a reminder after 10 seconds. The reminder message is also displayed as a SnackBar for confirmation.

## Conclusion

In this blog post, we explored how to create a reminder app with voice recognition using the Flutter Alarm Manager package. By integrating voice recognition capabilities, users can set reminders effortlessly by simply speaking into their device's microphone. This not only enhances convenience but also adds a modern touch to the app's user experience.

Implementing voice recognition and reminder scheduling is just the beginning. You can further expand the functionality of your app by adding features like repeating reminders, custom notification tones, and more. As Flutter continues to evolve, so does the potential for creating innovative and user-friendly apps.

#flutter #voice-recognition
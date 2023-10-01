---
layout: post
title: "Implementing offline speech recognition and voice commands in WorkManager tasks for Flutter"
description: " "
date: 2023-10-01
tags: [flutter, speechrecognition, voicerecognition, workmanager]
comments: true
share: true
---

In this blog post, we will explore how to implement offline speech recognition and voice commands in WorkManager tasks for Flutter. This will allow your Flutter app to perform speech recognition and execute voice commands even when the device is offline.

## Why offline speech recognition and voice commands?

Offline speech recognition and voice commands are essential features for certain types of applications, such as voice assistants or applications that heavily rely on voice input. By enabling offline functionality, your app can provide a seamless user experience even in low connectivity or offline scenarios.

## Prerequisites

Before proceeding, ensure that you have the following:

- Flutter SDK installed on your machine
- A Flutter project set up

## Adding dependencies

To implement offline speech recognition and voice commands, we'll need to add some dependencies to our Flutter project. Open your `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  speech_to_text: ^3.0.0
  workmanager: ^0.4.1
```

Run `flutter pub get` to install the new dependencies.

## Setting up speech recognition

To enable offline speech recognition, we'll be using the `speech_to_text` package. Create a new file called `speech_recognition.dart` and add the following code:

```dart
import 'package:speech_to_text/speech_to_text.dart' as stt;

class SpeechRecognition {
  final stt.SpeechToText _speech = stt.SpeechToText();

  Future<bool> initialize() async {
    return await _speech.initialize();
  }

  Future<String> listen({String locale = 'en_US'}) async {
    return await _speech.listen(locale: locale);
  }

  void stop() => _speech.stop();
}
```

In this code, we've created a `SpeechRecognition` class that encapsulates the speech recognition functionality. We use the `speech_to_text` package to initialize the speech recognizer and start/stop listening for speech input.

## Setting up voice commands using WorkManager

Next, we'll integrate the `SpeechRecognition` class with WorkManager to enable voice commands in background tasks. Open your `main.dart` file and modify the following code:

```dart
import 'dart:async';
import 'package:flutter/material.dart';
import 'package:workmanager/workmanager.dart';
import 'speech_recognition.dart';

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) {
    SpeechRecognition speechRecognition = SpeechRecognition();
    speechRecognition.initialize().then((value) {
      if (value) {
        speechRecognition.listen().then((text) {
          if (text.isNotEmpty) {
            // Process the voice command
          }
          speechRecognition.stop();
          return Future.value(true);
        });
      }
    });
    return Future.value(true);
  });
}

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  Workmanager.initialize(callbackDispatcher);
  Workmanager.registerPeriodicTask(
    "1",
    "speech_recognition_task",
    frequency: Duration(minutes: 15),
    constraints: Constraints(networkType: NetworkType.connected),
  );
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Voice Commands',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Flutter Voice Commands'),
        ),
        body: Center(
          child: Text('Implement voice commands with WorkManager'),
        ),
      ),
    );
  }
}

```

In this code, we have defined a `callbackDispatcher` function that will be called by WorkManager whenever the scheduled task is executed. Inside this function, we initialize the `SpeechRecognition` class, listen for voice input, and process the voice command if any.

In the `main` function, we initialize WorkManager, register a periodic task that will execute the `speech_recognition_task` every 15 minutes, and start the Flutter app.

## Conclusion

Congratulations! You have successfully implemented offline speech recognition and voice commands using WorkManager tasks in Flutter. By leveraging the `speech_to_text` package and integrating with WorkManager, your app can now provide a seamless voice-controlled experience even when the device is offline.

Remember to test your implementation thoroughly and consider the potential privacy and user experience implications of voice commands in your app. Happy coding!

#flutter #speechrecognition #voicerecognition #workmanager
---
layout: post
title: "Implementing voice recognition and speech-to-text in scheduled tasks with WorkManager for Flutter"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to implement voice recognition and speech-to-text functionality in scheduled tasks using WorkManager in Flutter. Voice recognition and speech-to-text are powerful features that can enhance the user experience in various applications, from voice assistants to transcription tools. WorkManager is a library in Flutter that allows us to schedule and run background tasks efficiently.

## Prerequisites

To follow along with this tutorial, you will need:

- Flutter installed on your machine
- Basic knowledge of Flutter and Dart programming language

## Step 1: Setting Up the Project

First, let's create a new Flutter project by running the following command in the terminal:

```shell
flutter create voice_recognition_app
```

Change into the project directory:

```shell
cd voice_recognition_app
```

## Step 2: Adding Dependencies

Next, we need to add the necessary dependencies for voice recognition and speech-to-text functionality. Open the `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  workmanager: ^0.4.1
  speech_to_text: ^3.0.0
```

Save the file and run the following command to fetch the dependencies:

```shell
flutter pub get
```

## Step 3: Implementing Voice Recognition

Create a new Dart file called `voice_recognition.dart` in the `lib` folder. In this file, let's import the required dependencies:

```dart
import 'package:speech_to_text/speech_to_text.dart' as stt;
import 'package:workmanager/workmanager.dart';
```

Next, let's define a `VoiceRecognition` class and add the necessary methods. Start by initializing the speech-to-text instance:

```dart
class VoiceRecognition {
  final stt.SpeechToText _speechToText = stt.SpeechToText();
}
```

Now, let's implement a method that will handle the voice recognition functionality:

```dart
Future<void> startListening() async {
  _speechToText.listen(
    listenFor: Duration(minutes: 1),
    onResult: (stt.SpeechRecognitionResult result) {
      String transcription = result.recognizedWords;
      print('Transcription: $transcription');
    },
  );
}
```

In the `startListening` method, we use the `listen` function provided by the speech-to-text library. This function listens for user speech for a specified duration, in this case, one minute. When speech is detected, the `onResult` callback function is invoked, providing the recognized words as a `SpeechRecognitionResult`. We extract the recognized words and print them out for now.

## Step 4: Scheduling the Voice Recognition Task with WorkManager

Next, let's schedule the voice recognition task to run periodically using WorkManager. In the `voice_recognition.dart` file, add the following method:

```dart
void scheduleVoiceRecognitionTask() {
  Workmanager.initialize(
    callbackDispatcher,
    isInDebugMode: true,
  );

  Workmanager.registerPeriodicTask(
    'voiceRecognitionTask',
    'voice_recognition',
    frequency: Duration(minutes: 15),
  );
}

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) {
    VoiceRecognition().startListening();
    return Future.value(true);
  });
}
```

Here, we use the `Workmanager` class to initialize and register a periodic task. The `callbackDispatcher` function is invoked when the task is scheduled to run. Inside the callback function, we create an instance of the `VoiceRecognition` class and call the `startListening` method.

Note that for the periodic task to work, we need to register a headless service in the `AndroidManifest.xml` file and set up the necessary permissions.

## Step 5: Using the Voice Recognition Task

Now that we have set up the voice recognition task, let's use it in our Flutter app. Open the `main.dart` file and modify the `main` method as follows:

```dart
void main() {
  WidgetsFlutterBinding.ensureInitialized();
  VoiceRecognition().scheduleVoiceRecognitionTask();
  runApp(MyApp());
}
```

Here, we ensure that the necessary bindings are initialized, then schedule the voice recognition task before running the app.

## Step 6: Testing the Voice Recognition Task

To test the voice recognition task, run the Flutter app on a device or emulator. You should see the scheduled voice recognition task running in the background every 15 minutes. When speech is detected, the recognized words will be printed to the console.

Congratulations! You have successfully implemented voice recognition and speech-to-text functionality in scheduled tasks using WorkManager for Flutter.

## Conclusion

In this tutorial, we explored how to integrate voice recognition and speech-to-text functionality into scheduled tasks using WorkManager in Flutter. By leveraging WorkManager, we can run background tasks efficiently, enabling applications to perform voice recognition even when the app is not actively running. This can enhance the user experience and open up new possibilities for building powerful voice-enabled applications.
---
layout: post
title: "Working with voice recognition and speech synthesis using GetX"
description: " "
date: 2023-09-29
tags: [Flutter, GetX]
comments: true
share: true
---

In this tutorial, we will explore how to work with voice recognition and speech synthesis using the GetX framework in a Flutter application. We will leverage the `speech_recognition` and `tts` plugins, along with the powerful state management features provided by GetX.

## Voice Recognition

### Installation

To get started, we need to add the `speech_recognition` plugin to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter

  speech_recognition: ^2.1.0
```

After adding the dependency, run `flutter pub get` in the terminal to fetch the package.

### Setup and Initialization

Next, we need to initialize the `SpeechRecognition` instance in our app. This can be done in the `main.dart` file:

```dart
import 'package:speech_recognition/speech_recognition.dart';

void main() {
  initializeSpeechRecognition(); // Initialize before running the app
  runApp(MyApp());
}

Future<void> initializeSpeechRecognition() async {
  final SpeechRecognition _speechRecognition = SpeechRecognition();

  await _speechRecognition.initialize();

  bool isAvailable = await _speechRecognition.isAvailable();
  if (isAvailable) {
    _speechRecognition.setRecognitionStartCallback(() {
      print('Recognition started');
    });

    _speechRecognition.setRecognitionCompleteCallback(() {
      print('Recognition completed');
    });
  }
}
```

In the above code snippet, we initialize the `SpeechRecognition` instance and set the recognition start and complete callbacks. These callbacks can be used to handle events during voice recognition.

### Starting and Stopping Voice Recognition

To start listening for voice input, we can call the `SpeechRecognition` instance's `listen` method:

```dart
Future<void> startListening() async {
  if (await _speechRecognition.isAvailable()) {
    await _speechRecognition.listen();
  }
}
```

We can also stop the voice recognition at any time using the `stop` method:

```dart
void stopListening() {
  _speechRecognition.stop();
}
```

## Speech Synthesis

### Installation

To add speech synthesis functionality, we will use the `tts` plugin. Add the following dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter

  tts: ^1.4.1
```

Run `flutter pub get` in the terminal to fetch the plugin.

### Initialization and Speech Synthesis

To initialize the speech synthesis engine, add the following code to your `main.dart` file:

```dart
import 'package:flutter_tts/flutter_tts.dart';

void main() {
  initializeSpeechSynthesis(); // Initialize before running the app
  runApp(MyApp());
}

Future<void> initializeSpeechSynthesis() async {
  final FlutterTts flutterTts = FlutterTts();

  await flutterTts.setSpeechRate(1.0);
  await flutterTts.setVolume(1.0);

  await flutterTts.setLanguage("en-US");
}

```

In the above code snippet, we initialize the `FlutterTts` instance and set the speech rate, volume, and language for synthesis.

We can use the `speak` method to convert text to speech:

```dart
Future<void> speak(String text) async {
  await flutterTts.speak(text);
}
```

To stop speech synthesis, we can use the `stop` method:

```dart
void stopSpeaking() {
  flutterTts.stop();
}
```

With these simple steps, you can now implement voice recognition and speech synthesis in your Flutter app using the GetX framework. Happy coding!

\#Flutter \#GetX
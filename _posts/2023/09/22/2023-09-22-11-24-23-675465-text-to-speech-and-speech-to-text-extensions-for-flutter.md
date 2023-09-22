---
layout: post
title: "Text-to-speech and speech-to-text extensions for Flutter"
description: " "
date: 2023-09-22
tags: [flutter, texttospeech]
comments: true
share: true
---

Flutter is a popular cross-platform framework for building mobile applications. With its rich set of APIs and customizable widgets, Flutter provides developers with the ability to create beautiful and responsive apps.

One area where Flutter excels is in supporting accessibility features, such as text-to-speech (TTS) and speech-to-text (STT) capabilities. By integrating TTS and STT into your Flutter app, you can enhance the user experience for individuals with visual impairments or those who prefer interacting with apps using their voice.

In this blog post, we will explore two popular extensions for adding TTS and STT features to your Flutter app:

## 1. flutter_tts

`flutter_tts` is a Flutter plugin that allows you to easily add TTS capabilities to your app. With `flutter_tts`, you can convert text into speech and have it read out loud to the user. This can be particularly useful for reading out article content, notifications, or any other textual information in your app.

To use `flutter_tts`, simply add it to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_tts: ^3.0.0
```

Once added, you can import the package in your Dart code and start using the TTS functionality:

```dart
import 'package:flutter_tts/flutter_tts.dart';

FlutterTts flutterTts = FlutterTts();

// Convert text to speech
await flutterTts.speak('Hello, world!');

// Adjust TTS settings
await flutterTts.setSpeechRate(0.5);
await flutterTts.setLanguage('en-US');
```

## 2. speech_to_text

The `speech_to_text` plugin enables speech recognition and transcription within your Flutter app. By integrating this extension, you can allow users to input text by speaking instead of typing, making your app more accessible and hands-free.

To use `speech_to_text`, add it to your `pubspec.yaml` file:

```yaml
dependencies:
  speech_to_text: ^5.0.0
```

To start using the STT functionality, import the package and initialize it in your code:

```dart
import 'package:speech_to_text/speech_to_text.dart' as stt;

stt.SpeechToText speech = stt.SpeechToText();

// Check if speech recognition is available
bool isAvailable = await speech.initialize();

// Start listening for speech input
if (isAvailable) {
  await speech.listen(
    listenFor: Duration(seconds: 10),
    pauseFor: Duration(seconds: 5),
    onResult: (result) {
      print('Transcription: ${result.recognizedWords}');
    },
  );
} else {
  print('Speech recognition not available');
}
```

By integrating these two extensions into your Flutter app, you can create a more inclusive experience for your users. Whether it's reading out text or transcribing speech, TTS and STT functionalities can greatly enhance the accessibility and usability of your app.

#flutter #texttospeech #speechtotext
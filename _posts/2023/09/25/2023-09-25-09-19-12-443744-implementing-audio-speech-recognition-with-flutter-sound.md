---
layout: post
title: "Implementing audio speech recognition with Flutter Sound"
description: " "
date: 2023-09-25
tags: [SpeechRecognition]
comments: true
share: true
---

In this tutorial, we will explore how to implement audio speech recognition using the Flutter Sound package. Speech recognition allows an application to convert spoken words into text, opening up a wide range of possibilities for voice commands and dictation features. Flutter Sound is a powerful audio manipulation package that provides easy access to the device's microphone and audio recording capabilities.

## Prerequisites

To follow along with this tutorial, you will need:

1. **Flutter** installed on your machine. You can find installation instructions on the [official Flutter website](https://flutter.dev/docs/get-started/install).
2. A text editor or an integrated development environment (IDE) like **Visual Studio Code** or **Android Studio**.

## Setting Up the Project

Let's start by creating a new Flutter project:

```dart
$ flutter create audio_speech_recognition
```

Once the project is created, open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter_sound: ^X.X.X # Replace with the latest version
```

Then, run the `flutter packages get` command to fetch the package.

## Implementing Audio Recording

First, we need to set up audio recording functionality to capture the user's speech. Create a new Dart file called `audio_recorder.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_sound/flutter_sound.dart';

class AudioRecorder extends StatefulWidget {
  @override
  _AudioRecorderState createState() => _AudioRecorderState();
}

class _AudioRecorderState extends State<AudioRecorder> {
  FlutterSoundPlayer _player = FlutterSoundPlayer();
  FlutterSoundRecorder _recorder = FlutterSoundRecorder();
  bool _isRecording = false;

  @override
  void dispose() {
    _player.closeAudioSession();
    _recorder.closeAudioSession();
    super.dispose();
  }

  Future<void> _startRecording() async {
    try {
      await _recorder.openAudioSession();
      await _recorder.startRecorder(toFile: 'audio_file.wav');
      setState(() => _isRecording = true);
    } catch (e) {
      print('Recording failed: $e');
    }
  }

  Future<void> _stopRecording() async {
    try {
      await _recorder.stopRecorder();
      await _recorder.closeAudioSession();
      setState(() => _isRecording = false);
    } catch (e) {
      print('Stopping recording failed: $e');
    }
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        RaisedButton(
          onPressed: _isRecording ? _stopRecording : _startRecording,
          child: Text(_isRecording ? 'Stop Recording' : 'Start Recording'),
        ),
      ],
    );
  }
}
```

The `AudioRecorder` widget controls the audio recording functionality. When the user taps the "Start Recording" button, we call the `_startRecording` method to open the audio session and start recording. When they tap the "Stop Recording" button, we call the `_stopRecording` method to stop recording and close the audio session.

## Implementing Speech Recognition

To implement speech recognition, we will use the **speech_to_text** package. Add the following dependency to the `pubspec.yaml` file:

```yaml
dependencies:
  speech_to_text: ^X.X.X # Replace with the latest version
```

Run `flutter packages get` to fetch the package. Then, in the `audio_recorder.dart` file, add the following code to the `_stopRecording` method:

```dart
import 'package:speech_to_text/speech_recognition_result.dart';
import 'package:speech_to_text/speech_to_text.dart' as stt;

// ...

Future<void> _stopRecording() async {
  try {
    // ...

    await _recorder.stopRecorder();
    await _recorder.closeAudioSession();
    setState(() => _isRecording = false);

    stt.SpeechToText speech = stt.SpeechToText();
    bool isAvailable = await speech.initialize();
    if (isAvailable) {
      speech.listen(
        onResult: (stt.SpeechRecognitionResult result) {
          String transcription = result.recognizedWords;
          print(transcription);
        },
      );
    } else {
      print('Speech recognition not available');
    }
  } catch (e) {
    print('Stopping recording failed: $e');
  }
}
```

We initialize the `speech_to_text` package and check if speech recognition is available on the device. If available, we start listening for the result using the `listen` method. The recognized words are provided in the `result.recognizedWords` property.

## Running the App

To use the `AudioRecorder` widget in your app, open the `lib/main.dart` file and update it as follows:

```dart
import 'package:flutter/material.dart';
import 'audio_recorder.dart';

void main() {
  runApp(AudioSpeechRecognitionApp());
}

class AudioSpeechRecognitionApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Audio Speech Recognition',
      home: Scaffold(
        appBar: AppBar(title: Text('Audio Speech Recognition')),
        body: AudioRecorder(),
      ),
    );
  }
}
```

Finally, save all your changes and run the app using the `flutter run` command in the terminal.

## Conclusion

By implementing audio speech recognition with Flutter Sound, we've added a powerful feature to our Flutter app that allows users to interact via voice commands. We can now capture audio recordings and convert speech into text, opening up countless opportunities for voice-driven applications. Explore the Flutter Sound and speech_to_text packages further to customize and enhance your speech recognition functionality. Happy coding!

## #Flutter #SpeechRecognition
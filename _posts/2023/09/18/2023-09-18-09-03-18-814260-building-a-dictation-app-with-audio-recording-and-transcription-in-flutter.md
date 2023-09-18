---
layout: post
title: "Building a dictation app with audio recording and transcription in Flutter"
description: " "
date: 2023-09-18
tags: [flutter, appdevelopment]
comments: true
share: true
---

In this tutorial, we will explore how to build a dictation app using Flutter. The app will allow users to record audio and transcribe it into text. We will utilize the audio recording and transcription capabilities provided by Flutter plugins to achieve this functionality.

## Prerequisites

Before we start, make sure you have Flutter installed on your system. You will also need a code editor of your choice.

## Setting up the Project

To begin, create a new Flutter project by running the following command in your terminal:

```bash
flutter create dictation_app
```

Change the directory to `dictation_app`:

```bash
cd dictation_app
```

Now, open the project in your code editor.

## Installing Dependencies

To record audio, we will use the `flutter_sound` plugin. Add the following dependency to your project's `pubspec.yaml` file:

```yaml
dependencies:
  flutter_sound: ^8.0.5
```

Save the file and run the following command to fetch the dependencies:

```bash
flutter pub get
```

## Setting up Audio Recording

First, we need to set up audio recording. Create a new file named `audio_recorder.dart`. Import the necessary dependencies:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_sound/flutter_sound.dart';
```

Inside the `AudioRecorder` widget, define a `FlutterSound` instance to handle audio recording:

```dart
class AudioRecorder extends StatefulWidget {
  @override
  _AudioRecorderState createState() => _AudioRecorderState();
}

class _AudioRecorderState extends State<AudioRecorder> {
  FlutterSoundRecorder _audioRecorder = FlutterSoundRecorder();
  //...
  // Rest of the code
}
```

Next, override the `initState` and `dispose` methods to initialize and dispose of the audio recorder object:

```dart
@override
void initState() {
  super.initState();
  _audioRecorder.openAudioSession().then((value) {
    print('Audio session opened');
  });
}

@override
void dispose() {
  _audioRecorder.closeAudioSession().then((value) {
    print('Audio session closed');
  });
  super.dispose();
}
```

Now, we can add methods to start and stop audio recording:

```dart
void _startRecording() async {
  await _audioRecorder.startRecorder(
    toFile: 'path/to/save/audio.wav',
    audioFormat: FlutterSoundAudioFormat.WAV,
  );
}

void _stopRecording() async {
  await _audioRecorder.stopRecorder();
}
```

## Transcribing Audio to Text

To transcribe the recorded audio to text, we will use the `speech_to_text` plugin. Add the following dependency to your `pubspec.yaml`:

```yaml
dependencies:
  speech_to_text: ^5.0.0
```

Inside the `AudioRecorder` widget, import the necessary dependencies:

```dart
import 'package:speech_to_text/speech_to_text.dart' as stt;
```

Define a `SpeechToText` instance to handle speech recognition:

```dart
class _AudioRecorderState extends State<AudioRecorder> {
  FlutterSoundRecorder _audioRecorder = FlutterSoundRecorder();
  stt.SpeechToText _speechToText = stt.SpeechToText();
  //...
  // Rest of the code
}
```

Add a method to transcribe the recorded audio:

```dart
void _transcribeAudio() async {
  String audioFilePath = 'path/to/save/audio.wav';
  String transcription = await _speechToText.recognize(
    audioFilePath: audioFilePath,
    onStatus: (String status) {
      print('Speech to text status: $status');
    },
  );
  print('Audio transcription: $transcription');
}
```

## User Interface

To provide a user interface for recording and transcribing audio, we can use Flutter's built-in widgets. Update the `AudioRecorder` widget's build method as follows:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text('Dictation App'),
    ),
    body: Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          RaisedButton(
            onPressed: _startRecording,
            child: Text('Start Recording'),
          ),
          RaisedButton(
            onPressed: _stopRecording,
            child: Text('Stop Recording'),
          ),
          RaisedButton(
            onPressed: _transcribeAudio,
            child: Text('Transcribe Audio'),
          ),
        ],
      ),
    ),
  );
}
```

## Running the App

To test the app, run the following command:

```bash
flutter run
```

Now you have a dictation app with audio recording and transcription functionality. Users can record audio and transcribe it into text with just a few taps.

#flutter #appdevelopment
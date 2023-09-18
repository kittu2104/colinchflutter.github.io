---
layout: post
title: "Recording and playback of live radio broadcasts in a Flutter app"
description: " "
date: 2023-09-18
tags: [flutter, radio]
comments: true
share: true
---

Flutter is becoming a popular choice for building cross-platform mobile applications. One interesting use case for Flutter is creating apps that allow users to listen to live radio broadcasts. In this article, we will explore how to implement the recording and playback functionality for live radio broadcasts in a Flutter app.

## Requirements

To implement the recording and playback functionality for live radio broadcasts, we will require the following:

- Flutter SDK installed on your machine
- Dart programming language knowledge
- Audio recording and playback libraries for Flutter

## Implementation Steps

### 1. Setting up Flutter Project

Create a new Flutter project using the following command:

```dart
flutter create radio_app
```

Navigate to the newly created project:

```dart
cd radio_app
```

### 2. Adding Dependencies

Open the `pubspec.yaml` file and add the required dependencies for audio recording and playback:

```dart
dependencies:
  flutter:
    sdk: flutter

  flutter_sound: ^8.0.4
  just_audio: ^0.7.0
```

Save the changes and run the following command to fetch the dependencies:

```dart
flutter packages get
```

### 3. Recording Audio

To record audio, we will use the `flutter_sound` library. Create a new Dart file called `audio_recorder.dart` and implement the audio recording logic:

```dart
import 'package:flutter_sound/flutter_sound.dart';
import 'package:path_provider/path_provider.dart';

class AudioRecorder {
  FlutterSoundRecorder _recorder;
  String _recordingPath;

  Future<void> startRecording() async {
    final appDir = await getApplicationDocumentsDirectory();
    _recordingPath = '${appDir.path}/recording.wav';

    _recorder = FlutterSoundRecorder();
    await _recorder.openAudioSession();
    await _recorder.startRecorder(toFile: _recordingPath);
  }

  Future<void> stopRecording() async {
    await _recorder.stopRecorder();
    await _recorder.closeAudioSession();
  }

  String get recordingPath => _recordingPath;
}
```

### 4. Playback Audio

For audio playback, we will use the `just_audio` library. Create a new Dart file called `audio_player.dart` and implement the audio playback logic:

```dart
import 'package:just_audio/just_audio.dart';

class AudioPlayer {
  AudioPlayer _player;

  Future<void> playAudio(String audioPath) async {
    _player = AudioPlayer();
    await _player.setUrl(audioPath);
    await _player.play();
  }

  Future<void> stopAudio() async {
    await _player.stop();
  }
}
```

### 5. Integrating in the Flutter App

In your main Flutter app, import the `audio_recorder.dart` and `audio_player.dart` files, and use the `AudioRecorder` and `AudioPlayer` classes to record and playback the audio.

```dart
import 'package:flutter/material.dart';
import 'audio_recorder.dart';
import 'audio_player.dart';

void main() {
  runApp(RadioApp());
}

class RadioApp extends StatelessWidget {
  final AudioRecorder _audioRecorder = AudioRecorder();
  final AudioPlayer _audioPlayer = AudioPlayer();

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Radio App',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Radio App'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              RaisedButton(
                onPressed: () {
                  _audioRecorder.startRecording();
                },
                child: Text('Start Recording'),
              ),
              RaisedButton(
                onPressed: () {
                  _audioRecorder.stopRecording().then((_) {
                    _audioPlayer.playAudio(_audioRecorder.recordingPath);
                  });
                },
                child: Text('Stop Recording & Play'),
              ),
              RaisedButton(
                onPressed: () {
                  _audioPlayer.stopAudio();
                },
                child: Text('Stop Playback'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

### Summary

In this article, we learned how to implement the recording and playback functionality for live radio broadcasts in a Flutter app. We used the `flutter_sound` library for audio recording and `just_audio` library for audio playback. By integrating these libraries into a Flutter app, users can conveniently listen to live radio broadcasts and even record them for later playback.

#flutter #radio #app #audio #recording #playback
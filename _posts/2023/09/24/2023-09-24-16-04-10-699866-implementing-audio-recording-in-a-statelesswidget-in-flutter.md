---
layout: post
title: "Implementing audio recording in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [audio, recording, FlutterDevelopment, appdevelopment]
comments: true
share: true
---

Flutter makes it easy to implement audio recording functionality in your app. In this tutorial, you will learn how to record audio using the microphone and save it to a file using a StatelessWidget.

## Prerequisites

Before diving into the implementation, make sure you have Flutter installed on your machine. You will also need an IDE or code editor of your choice to write the Flutter code.

## Step 1: Add Dependencies

Open your Flutter project and navigate to the `pubspec.yaml` file. Add the following dependencies under the `dependencies` section:

```yaml
dependencies:
  flutter:
    sdk: flutter
  permission_handler: ^12.1.0
  flutter_sound_lite: ^2.0.1
```

Save the file and run `flutter pub get` to install the dependencies.

## Step 2: Request Microphone Permission

To record audio, you need to request permission to access the device's microphone. Create a new file called `audio_permission.dart` and add the following code:

```dart
import 'package:permission_handler/permission_handler.dart';

class AudioPermission {
  Future<bool> requestMicrophonePermission() async {
    var microphonePermissionStatus = await Permission.microphone.request();
    return microphonePermissionStatus.isGranted;
  }
}
```

This code creates a helper class `AudioPermission` that requests microphone permission using the `permission_handler` package. It returns `true` if the permission is granted, and `false` otherwise.

## Step 3: Create Recording Screen

Create a new file called `recording_screen.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_sound_lite/flutter_sound.dart';

class RecordingScreen extends StatelessWidget {
  final FlutterSoundRecorder _soundRecorder = FlutterSoundRecorder();

  @override
  void dispose() {
    _soundRecorder.stopRecorder();
    _soundRecorder.closeAudioSession();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Audio Recorder')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: _startRecording,
              child: Text('Start Recording'),
            ),
            ElevatedButton(
              onPressed: _stopRecording,
              child: Text('Stop Recording'),
            ),
          ],
        ),
      ),
    );
  }

  void _startRecording() async {
    await _soundRecorder.openAudioSession();
    await _soundRecorder.startRecorder(toFile: 'audio_recording.aac', codec: Codec.aacMP4);
  }

  void _stopRecording() async {
    await _soundRecorder.stopRecorder();
    await _soundRecorder.closeAudioSession();
  }
}
```

In this code, we create a new class `RecordingScreen` which extends `StatelessWidget`. Inside the class, we create an instance of `FlutterSoundRecorder` which will handle the audio recording functionality.

The `build` method returns a simple UI with two buttons: "Start Recording" and "Stop Recording". The `_startRecording` method starts the recording session and saves the recorded audio to a file. The `_stopRecording` method stops the recording session.

The `dispose` method is overridden to stop the recording and close the audio session when the widget is disposed.

## Step 4: Implement Navigation

To test the recording screen, navigate to your `main.dart` file and add the following code:

```dart
import 'package:flutter/material.dart';
import 'recording_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Audio Recording',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => RecordingScreen()),
            );
          },
          child: Text('Go to Recording Screen'),
        ),
      ),
    );
  }
}
```

In this code, we create a `HomeScreen` widget that navigates to the `RecordingScreen` widget when a button is pressed.

## Conclusion

Congratulations! You have successfully implemented audio recording in a StatelessWidget in Flutter. This functionality can be a great addition to your app, allowing users to record and save audio files. Remember to handle permission requests and manage the recording lifecycle properly for a polished user experience.

#flutter #audio #recording #FlutterDevelopment #appdevelopment
---
layout: post
title: "Building a music-making app with audio recording and playback in Flutter"
description: " "
date: 2023-09-18
tags: [flutter, musicapp]
comments: true
share: true
---

Flutter is a powerful framework for building cross-platform apps. Whether you are a musician or a music enthusiast, creating a music-making app can be an exciting project. In this tutorial, we will explore how to build a music-making app in Flutter that allows users to record and play audio.

## Getting Started with Flutter

To begin, make sure you have Flutter installed on your machine. If you haven't installed Flutter yet, you can follow the official installation guide on the Flutter website.

## Setting Up the Project

Open your terminal and create a new Flutter project using the following command:

```sh
flutter create music_app
```

Once the project is created, navigate to the project directory:

```sh
cd music_app
```

## Adding Dependencies

To handle audio recording and playback, we will need to add the following dependencies to the `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter

  audioplayers: ^0.21.2
  just_audio: ^0.9.11
  permission_handler: ^8.0.0 
  path_provider: ^2.0.5
  fluttertoast: ^8.0.8
```

Run the following command to install the dependencies:

```sh
flutter pub get
```

## Creating the User Interface

In this example, we will create a simple user interface with two buttons - one for recording audio and one for playing it back. Create a new file, `main.dart`, and replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MusicApp());
}

class MusicApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Music App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MusicScreen(),
    );
  }
}

class MusicScreen extends StatefulWidget {
  @override
  _MusicScreenState createState() => _MusicScreenState();
}

class _MusicScreenState extends State<MusicScreen> {
  bool isRecording = false;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Music App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: () {
                setState(() {
                  isRecording = !isRecording;
                });
              },
              child: Text(
                isRecording ? 'Stop Recording' : 'Start Recording',
              ),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                // TODO: Play audio
              },
              child: Text('Play'),
            ),
          ],
        ),
      ),
    );
  }
}
```

## Implementing Audio Recording

To enable audio recording, we need to request permission from the user. Add the following method to the `_MusicScreenState` class:

```dart
import 'package:permission_handler/permission_handler.dart';

Future<void> _requestRecordingPermission() async {
  PermissionStatus status = await Permission.microphone.request();
  if (status.isGranted) {
    // TODO: Start recording audio
  } else {
    // TODO: Handle permission denied
  }
}
```

Call this method when the user taps the record button:

```dart
onPressed: () {
  setState(() {
    isRecording = !isRecording;
  });
  if (isRecording) {
    _requestRecordingPermission();
  } else {
    // TODO: Stop recording audio
  }
},
```

## Recording Audio
 
To record audio, we will use the `just_audio` package. Add the following code to the `_MusicScreenState` class:

```dart
import 'package:just_audio/just_audio.dart';
import 'package:path/path.dart' as path;
import 'package:path_provider/path_provider.dart' as path_provider;

final _player = AudioPlayer();

Future<void> _startRecording() async {
  final directory = await path_provider.getTemporaryDirectory();
  final filePath = path.join(directory.path, 'recording.wav');

  await _player.setFilePath(filePath);
  await _player.record();
}

Future<void> _stopRecording() async {
  await _player.stop();
}
```

Call these methods accordingly when recording starts or stops:

```dart
if (isRecording) {
  _requestRecordingPermission();
  _startRecording();
} else {
  _stopRecording();
}
```

## Implementing Audio Playback

To play back the recorded audio, add the following code to the `_MusicScreenState` class:

```dart
Future<void> _playAudio() async {
  final directory = await path_provider.getTemporaryDirectory();
  final filePath = path.join(directory.path, 'recording.wav');

  await _player.setFilePath(filePath);
  await _player.play();
}

```

Call the `_playAudio()` method when the user taps the play button:

```dart
onPressed: () {
  _playAudio();
},
```

## Conclusion

In this tutorial, you learned how to build a music-making app with audio recording and playback using Flutter. You explored how to handle audio recording permission, record audio using the `just_audio` package, and play back the recorded audio. With this foundation, you can further enhance your app by adding features like editing audio, adding effects, and more.

Start building your own music-making app with Flutter today and unleash your creativity!

---
Tags: #flutter #musicapp
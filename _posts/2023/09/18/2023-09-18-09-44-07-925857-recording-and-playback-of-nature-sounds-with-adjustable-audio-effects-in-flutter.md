---
layout: post
title: "Recording and playback of nature sounds with adjustable audio effects in Flutter"
description: " "
date: 2023-09-18
tags: [audio]
comments: true
share: true
---

Flutter is a popular framework for building cross-platform apps, enabling developers to create beautiful and performant user experiences. In this blog post, we will explore how to implement recording and playback of nature sounds with adjustable audio effects using Flutter.

## Setting Up the Project

Before we dive into the implementation details, let's set up our Flutter project:

1. Create a new Flutter project by running the command `flutter create nature_sounds_app`.
2. Open the project in your preferred IDE.

## Recording Audio

To record audio in Flutter, we can leverage the `just_audio` package. This package provides a simple and easy-to-use API for handling audio playback. Add `just_audio` as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  just_audio: ^0.11.0
```

Next, let's implement the recording functionality in our app:

```dart
import 'package:flutter/material.dart';
import 'package:just_audio/just_audio.dart';
import 'package:path_provider/path_provider.dart';
import 'package:permission_handler/permission_handler.dart';

class RecordingScreen extends StatefulWidget {
  @override
  _RecordingScreenState createState() => _RecordingScreenState();
}

class _RecordingScreenState extends State<RecordingScreen> {
  AudioRecorder _recorder = AudioRecorder();
  AudioPlayer _player = AudioPlayer();
  Recording _currentRecording;
  String _recordingPath;

  @override
  void initState() {
    super.initState();
    _initializeRecorder();
  }

  Future<void> _initializeRecorder() async {
    if (await Permission.microphone.request().isGranted) {
      final appDir = await getApplicationDocumentsDirectory();
      _recordingPath = appDir.path + '/recording.wav';

      await _recorder.initialize(
        outputFormat: OutputFormat.wav,
        audioSource: AudioSource.microphone,
        outputPath: _recordingPath,
      );
    }
  }

  Future<void> _startRecording() async {
    if (await Permission.microphone.request().isGranted) {
      await _recorder.start();
    }
  }

  Future<void> _stopRecording() async {
    if (await _recorder.isRecording) {
      _currentRecording = await _recorder.stop();
    }
  }

  @override
  void dispose() {
    _recorder.dispose();
    _player.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Recording')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            RaisedButton(
              child: Text('Start Recording'),
              onPressed: _startRecording,
            ),
            RaisedButton(
              child: Text('Stop Recording'),
              onPressed: _stopRecording,
            ),
          ],
        ),
      ),
    );
  }
}
```

In the code above, we create a `RecordingScreen` widget that sets up the necessary dependencies and provides buttons to start and stop the recording. We use the `AudioRecorder` class from the `just_audio` package to handle audio recording.

## Playback with Adjustable Audio Effects

To add adjustable audio effects to our nature sounds playback, we can utilize the `flutter_sound` package. This package provides a wide range of audio manipulation options, including changing the pitch, speed, and volume.

Add `flutter_sound` as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_sound: ^8.0.1
```

We can now modify our existing code to include playback functionality with adjustable audio effects:

```dart
import 'package:flutter_sound/flutter_sound.dart';

class PlaybackScreen extends StatefulWidget {
  @override
  _PlaybackScreenState createState() => _PlaybackScreenState();
}

class _PlaybackScreenState extends State<PlaybackScreen> {
  FlutterSoundPlayer _player = FlutterSoundPlayer();
  double _volume = 1.0;
  double _pitch = 1.0;
  double _speed = 1.0;

  Future<void> _startPlayback() async {
    final appDir = await getApplicationDocumentsDirectory();
    final recordingPath = appDir.path + '/recording.wav';

    await _player.openAudioSession();
    await _player.setSubscriptionDuration(Duration(milliseconds: 16));

    await _player.startPlayer(
      fromURI: recordingPath,
      codec: Codec.pcm16WAV,
      whenFinished: () {
        // Playback finished
      },
    );
  }

  Future<void> _stopPlayback() async {
    await _player.stopPlayer();
    await _player.closeAudioSession();
  }

  void _setVolume(double value) {
    setState(() {
      _volume = value;
    });
    _player.setVolume(value);
  }

  void _setPitch(double value) {
    setState(() {
      _pitch = value;
    });
    _player.setPitch(value);
  }

  void _setSpeed(double value) {
    setState(() {
      _speed = value;
    });
    _player.setSpeed(value);
  }

  @override
  void dispose() {
    _player.closeAudioSession();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Playback')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            RaisedButton(
              child: Text('Start Playback'),
              onPressed: _startPlayback,
            ),
            RaisedButton(
              child: Text('Stop Playback'),
              onPressed: _stopPlayback,
            ),
            Slider(
              value: _volume,
              min: 0.0,
              max: 1.0,
              onChanged: _setVolume,
            ),
            Slider(
              value: _pitch,
              min: 0.5,
              max: 2.0,
              onChanged: _setPitch,
            ),
            Slider(
              value: _speed,
              min: 0.5,
              max: 2.0,
              onChanged: _setSpeed,
            ),
          ],
        ),
      ),
    );
  }
}
```

In the code above, we create a `PlaybackScreen` widget that handles the playback of the recorded audio. We use the `FlutterSoundPlayer` class from the `flutter_sound` package to play the audio file and adjust the volume, pitch, and speed.

## Conclusion

In this blog post, we learned how to implement recording and playback of nature sounds with adjustable audio effects in Flutter. With the help of the `just_audio` and `flutter_sound` packages, we were able to easily handle audio recording, playback, and manipulation. Flutter provides a powerful and versatile platform for building multimedia applications, and with these techniques, you can create immersive experiences for your users.

#flutter #audio #natureSounds #just_audio #flutter_sound
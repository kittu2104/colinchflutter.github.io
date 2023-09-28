---
layout: post
title: "Implementing audio recording with audio visualization using Flutter Sound"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

Flutter Sound is a powerful audio recording and playback library for Flutter applications. In this tutorial, we will explore how to use Flutter Sound to implement audio recording with audio visualization in a Flutter app.

## Getting Started

To get started, you'll need to add the `flutter_sound` package to your Flutter project. Open your `pubspec.yaml` file and add the following line to the `dependencies` section:

```yaml
dependencies:
  flutter_sound: ^2.0.0
```

Then, run the following command to fetch the package:

```bash
flutter pub get
```

## Recording Audio

First, let's start by creating a basic Flutter app with a button to start and stop recording. Here's an example of a simple app structure:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_sound/flutter_sound.dart';

void main() {
  runApp(AudioRecorderApp());
}

class AudioRecorderApp extends StatefulWidget {
  @override
  _AudioRecorderAppState createState() => _AudioRecorderAppState();
}

class _AudioRecorderAppState extends State<AudioRecorderApp> {
  FlutterSoundRecorder? _audioRecorder;
  bool _isRecording = false;

  @override
  void initState() {
    super.initState();
    _audioRecorder = FlutterSoundRecorder();
  }

  @override
  void dispose() {
    _audioRecorder?.release();
    super.dispose();
  }

  Future<void> _startRecording() async {
    await _audioRecorder?.startRecorder(toFile: 'audio.wav');
    setState(() {
      _isRecording = true;
    });
  }

  Future<void> _stopRecording() async {
    await _audioRecorder?.stopRecorder();
    setState(() {
      _isRecording = false;
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Audio Recorder'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              _isRecording
                  ? CircularProgressIndicator()
                  : ElevatedButton(
                      onPressed: _startRecording,
                      child: Text('Start Recording'),
                    ),
              SizedBox(height: 16),
              if (_isRecording)
                ElevatedButton(
                  onPressed: _stopRecording,
                  child: Text('Stop Recording'),
                ),
            ],
          ),
        ),
      ),
    );
  }
}
```

In the code above, we create a simple app with two buttons: one to start recording, and another to stop recording. When the "Start Recording" button is pressed, the `_startRecording` function is called, which initializes the audio recorder and starts recording to a file named `audio.wav`. When the "Stop Recording" button is pressed, the `_stopRecording` function is called, which stops the recording process.

## Visualizing Audio

To add audio visualization to the recording screen, we can use the `flutter_visualizers` package. Add the following line to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_visualizers: ^0.1.0
```

Run `flutter pub get` to fetch the package.

Now, let's modify our app to include an audio visualization widget. Here's an example of how to add a bar visualizer to our app:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_sound/flutter_sound.dart';
import 'package:flutter_visualizers/flutter_visualizers.dart';

void main() {
  runApp(AudioRecorderApp());
}

class AudioRecorderApp extends StatefulWidget {
  @override
  _AudioRecorderAppState createState() => _AudioRecorderAppState();
}

class _AudioRecorderAppState extends State<AudioRecorderApp> {
  FlutterSoundRecorder? _audioRecorder;
  bool _isRecording = false;

  @override
  void initState() {
    super.initState();
    _audioRecorder = FlutterSoundRecorder();
  }

  @override
  void dispose() {
    _audioRecorder?.release();
    super.dispose();
  }

  Future<void> _startRecording() async {
    await _audioRecorder?.startRecorder(toFile: 'audio.wav');
    setState(() {
      _isRecording = true;
    });
  }

  Future<void> _stopRecording() async {
    await _audioRecorder?.stopRecorder();
    setState(() {
      _isRecording = false;
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Audio Recorder'),
        ),
        body: Column(
          crossAxisAlignment: CrossAxisAlignment.center,
          children: [
            Expanded(
              child: Container(
                color: Colors.grey[200],
                child: _isRecording ? BarVisualizer() : Container(),
              ),
            ),
            ElevatedButton(
              onPressed: _isRecording ? _stopRecording : _startRecording,
              child: Text(_isRecording ? 'Stop Recording' : 'Start Recording'),
            ),
          ],
        ),
      ),
    );
  }
}
```

In the code above, we added a `Container` widget with the `BarVisualizer` as its child. The `BarVisualizer` visualizes the audio waveform in the form of bars. When the user starts recording, the visualization will be displayed. When the recording stops, the visualization will disappear.

## Conclusion

In this tutorial, we explored how to implement audio recording with audio visualization using Flutter Sound and the flutter_visualizers package. By following these examples, you can easily add audio recording and visualization capabilities to your Flutter applications. Have fun experimenting and building amazing audio-related features!
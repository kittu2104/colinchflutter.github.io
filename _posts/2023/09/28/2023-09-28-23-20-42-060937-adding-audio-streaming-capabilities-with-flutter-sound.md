---
layout: post
title: "Adding audio streaming capabilities with Flutter Sound"
description: " "
date: 2023-09-28
tags: [audio, streaming]
comments: true
share: true
---

Flutter Sound is a powerful audio recording and playback library for Flutter applications. It provides a simple and efficient way to add audio streaming capabilities to your Flutter app. In this tutorial, we will guide you through the process of integrating Flutter Sound into your project and demonstrate how to stream audio in real-time.

## Requirements

To follow along with this tutorial, you will need:

- Flutter SDK installed on your machine
- Basic knowledge of Flutter app development

## Installation

To begin, create a new Flutter project if you haven't already. Open your project in your favorite IDE and open the `pubspec.yaml` file. Add the following line to the `dependencies` section:

```yaml
flutter_sound: ^x.x.x
```

Replace `x.x.x` with the latest version of the Flutter Sound package. Save the file and run the following command in your terminal to fetch the updated dependencies:

```bash
$ flutter pub get
```

## Recording audio

To record audio using Flutter Sound, you can utilize the `Recorder` class. Add the following code snippet to your Dart file:

```dart
import 'package:flutter_sound/flutter_sound.dart';

class AudioRecorder {
  FlutterSoundRecorder? _recorder;

  Future<void> startRecording() async {
    _recorder = FlutterSoundRecorder();
    await _recorder!.openAudioSession();
    await _recorder!.startRecorder(toFile: 'path_to_save_recording');
  }

  Future<void> stopRecording() async {
    await _recorder!.stopRecorder();
    await _recorder!.closeAudioSession();
  }
}
```

Replace `'path_to_save_recording'` with the desired location to save your audio recordings.

## Playing audio

To play audio using Flutter Sound, you can use the `AudioPlayer` class. Add the following code snippet to your Dart file:

```dart
import 'package:flutter_sound/flutter_sound.dart';

class AudioPlayer {
  FlutterSoundPlayer? _player;

  Future<void> startPlaying(String audioPath) async {
    _player = FlutterSoundPlayer();
    await _player!.openAudioSession();
    await _player!.startPlayer(fromURI: audioPath);
  }
  
  Future<void> stopPlaying() async {
    await _player!.stopPlayer();
    await _player!.closeAudioSession();
  }
}
```

## Streaming audio

To stream audio in real-time, you can combine the recording and playing capabilities of Flutter Sound. Here's an example:

```dart
import 'package:flutter_sound/flutter_sound.dart';

class AudioStreamer {
  FlutterSoundRecorder? _recorder;
  FlutterSoundPlayer? _player;

  Future<void> startStreaming() async {
    _recorder = FlutterSoundRecorder();
    _player = FlutterSoundPlayer();

    await _recorder!.openAudioSession();
    await _recorder!.startRecorder();

    await _player!.openAudioSession();
    await _player!.startPlayer();

    _recorder!.interruptionHandler = () {
      _player!.stopPlayer();
    };
  }

  Future<void> stopStreaming() async {
    await _recorder!.stopRecorder();
    await _recorder!.closeAudioSession();

    await _player!.stopPlayer();
    await _player!.closeAudioSession();
  }
}
```

In this example, the `startStreaming` method starts both the recorder and player. The `interruptionHandler` is triggered when an interruption occurs, such as an incoming phone call or audio from another app. It stops the player to handle the interruption gracefully.

## Conclusion

Congratulations! You have successfully integrated Flutter Sound into your Flutter app and learned how to add audio streaming capabilities. With Flutter Sound, you can easily record, play, and stream audio in your applications. Feel free to explore the Flutter Sound documentation for additional features and customization options.

#flutter #audio #streaming
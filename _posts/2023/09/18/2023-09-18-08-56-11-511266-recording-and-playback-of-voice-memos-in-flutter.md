---
layout: post
title: "Recording and playback of voice memos in Flutter"
description: " "
date: 2023-09-18
tags: [VoiceMemos]
comments: true
share: true
---

Flutter is a powerful framework for building cross-platform mobile applications. With its rich set of libraries and plugins, you can easily implement various functionalities in your app. In this tutorial, we will explore how to record and playback voice memos in Flutter using the `audioplayers` plugin.

## Getting Started

To get started, create a new Flutter project and add the `audioplayers` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  audioplayers: ^0.19.0
```

After running `flutter pub get`, you're ready to implement voice recording and playback functionality in your Flutter app.

## Recording Voice Memos

To record voice memos, we'll utilize the `audioplayers` plugin along with the `audio_recorder` package.

First, import the necessary packages in your Dart file:

```dart
import 'package:audioplayers/audioplayers.dart';
import 'package:audio_recorder/audio_recorder.dart';
import 'package:path_provider/path_provider.dart';
```

Next, define a variable to store the path of the recorded audio file:

```dart
String _recordingPath = '';
```

To start recording, use the `AudioRecorder.start()` method:

```dart
void startRecording() async {
  bool hasPermissions = await AudioRecorder.hasPermissions;
  if (hasPermissions) {
    String path = (await getTemporaryDirectory()).path;
    String fullPath = '$path/recording.wav';
    await AudioRecorder.start(path: fullPath);
    setState(() {
      _recordingPath = fullPath;
    });
  } else {
    // Handle permissions not granted
  }
}
```

This function performs a check to ensure that the necessary permissions are granted before starting the recording. If permissions are not granted, you can handle the scenario accordingly.

## Playback Voice Memos

To playback the recorded voice memo, we'll use the `audioplayers` plugin. Import it in your Dart file:

```dart
import 'package:audioplayers/audioplayers.dart';
```

Next, define an instance of the `AudioPlayer` class:

```dart
AudioPlayer _audioPlayer = AudioPlayer();
```

To play the recorded audio, use the `AudioPlayer.play()` method:

```dart
void playRecording() {
  _audioPlayer.play(_recordingPath, isLocal: true);
}
```

This function takes the path of the recorded audio file and plays it using the `AudioPlayer`. Make sure to set the `isLocal` parameter to `true` when playing local files.

## Conclusion

With the `audioplayers` plugin, recording and playback of voice memos in Flutter becomes a breeze. You can easily integrate this functionality into your Flutter app, whether it's for voice messaging, recording notes, or any other use case that requires audio recording and playback.

Happy coding! #Flutter #VoiceMemos
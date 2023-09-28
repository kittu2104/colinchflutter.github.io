---
layout: post
title: "Implementing audio recording with customizable file formats in Flutter Sound"
description: " "
date: 2023-09-28
tags: [flutter, audiostreaming]
comments: true
share: true
---

In today's digital world, audio recording plays a vital role in various applications such as language learning apps, voice messaging apps, or audio transcription services. Flutter Sound is a powerful package for recording audio in Flutter applications. However, by default, it saves the recorded audio in the WAV file format. In this blog post, we will explore how to implement audio recording with customizable file formats using Flutter Sound.

## Getting Started with Flutter Sound

First, let's start by adding the Flutter Sound package to your Flutter project. Open your project's `pubspec.yaml` file and add the following dependency:

```dart
dependencies:
  flutter_sound: ^X.Y.Z  # Replace with the latest version of Flutter Sound
```

Run `flutter pub get` to fetch and add the dependency to your project.

## Recording Audio in Flutter

To record audio in Flutter, we need to use the `FlutterSoundRecorder` class provided by the `flutter_sound` package. Here's an example of how to initialize the recorder and start recording:

```dart
import 'package:flutter_sound/flutter_sound.dart';

final FlutterSoundRecorder _recorder = FlutterSoundRecorder();

void startRecording() async {
  await _recorder.openAudioSession();
  await _recorder.startRecorder(
    toFile: 'path/to/recording.wav',
    codec: Codec.pcm16,
  );
}

void stopRecording() async {
  await _recorder.stopRecorder();
  await _recorder.closeAudioSession();
}
```

In the code snippet above, we create an instance of `FlutterSoundRecorder` and use the `openAudioSession` method to initialize the recorder. We then use the `startRecorder` method to start recording audio and specify the file path and codec (WAV in this case). To stop the recording, we call the `stopRecorder` method and close the audio session using `closeAudioSession`.

## Customizing the File Format

To customize the file format for the recorded audio, we can use the `codec` parameter in the `startRecorder` method. The `codec` parameter accepts values from the `Codec` enum, which includes various audio codec options such as MP3, AAC, FLAC, and more.

Here's an example of recording audio in the MP3 file format:

```dart
void startRecordingMp3() async {
  await _recorder.openAudioSession();
  await _recorder.startRecorder(
    toFile: 'path/to/recording.mp3',
    codec: Codec.mp3,
  );
}
```

In the code above, we simply change the file extension from `.wav` to `.mp3` and set the `codec` parameter to `Codec.mp3`.

## Conclusion

In this blog post, we've seen how to implement audio recording with customizable file formats using Flutter Sound. By default, Flutter Sound saves the recorded audio in the WAV file format, but we can easily customize it to other popular formats such as MP3, AAC, or FLAC by using the appropriate codec. This allows us to optimize the file size and compatibility based on our application's needs.

With Flutter Sound, recording audio in Flutter becomes a breeze, opening up a world of possibilities for building innovative and feature-rich audio-related applications.

#flutter #audiostreaming
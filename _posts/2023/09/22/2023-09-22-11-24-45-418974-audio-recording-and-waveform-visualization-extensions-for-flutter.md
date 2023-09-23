---
layout: post
title: "Audio recording and waveform visualization extensions for Flutter"
description: " "
date: 2023-09-22
tags: [coding, FlutterExtensions]
comments: true
share: true
---

Flutter is a versatile cross-platform toolkit that allows developers to build beautiful and performant apps for mobile, web, and desktop. If you're looking to add audio recording and waveform visualization capabilities to your Flutter app, you're in luck! There are several excellent extensions available that make it easy to implement these features. In this article, we'll explore two popular extensions that can help you achieve your goals.

## 1. flutter_sound

[flutter_sound](https://pub.dev/packages/flutter_sound) is a powerful audio recording and playback library for Flutter. It provides a simple and intuitive API to record audio from the device's microphone and save it as a file. Additionally, it supports recording from custom input sources, such as audio streams.

To incorporate flutter_sound into your project, add the package to your `pubspec.yml` file:

```yaml
dependencies:
  flutter_sound: ^x.x.x
```

Import the package into your Dart file:

```dart
import 'package:flutter_sound/flutter_sound.dart';
```

Then, you can start using flutter_sound to capture audio:

```dart
FlutterSoundRecorder recorder = FlutterSoundRecorder();
recorder.openAudioSession().then((value) {
  recorder.startRecorder(
    codec: Codec.aacADTS,
    toFile: 'path/to/save/recording.aac',
  );
});

// Stop the recording
recorder.stopRecorder().then((value) {
  // Do something with the recorded audio file
});
```

By using flutter_sound, you can easily record audio and save it in various formats like AAC, ADTS, MP3, and more.

## 2. audiowave

[audiowave](https://pub.dev/packages/audiowave) is a Flutter package that enables you to create beautiful waveform visualizations from audio files. It uses a custom painter to draw the waveform and supports customization options such as color, background, zoom level, and more.

To get started with audiowave, add the package to your `pubspec.yml` file:

```yaml
dependencies:
  audiowave: ^x.x.x
```

Import the package into your Dart file:

```dart
import 'package:audiowave/audiowave.dart';
```

Then, you can use the `AudioWave` widget to display the waveform visualization:

```dart
AudioWave(
  url: 'path/to/audio/file.mp3',
  height: 200,
  spacing: 2.0,
  color: Colors.blue,
  backgroundColor: Colors.grey[300],
  borderRadius: BorderRadius.circular(8.0),
);
```

With audiowave, you can easily showcase the waveform of audio files in your Flutter app, providing a visually appealing experience to your users.

## Conclusion

With the flutter_sound and audiowave extensions, you can easily add audio recording and waveform visualization features to your Flutter app. Whether you need to capture audio from the microphone or display a stunning visual representation of audio files, these extensions have got you covered. So go ahead, explore these packages, and take your Flutter app to the next level!

#coding #FlutterExtensions
---
layout: post
title: "Implementing audio noise suppression with Flutter Sound"
description: " "
date: 2023-09-29
tags: []
comments: true
share: true
---

In this blog post, we will explore how to implement audio noise suppression in a Flutter application using the Flutter Sound package. Audio noise suppression is a technique used to remove background noise from an audio signal, providing a cleaner and clearer audio experience to the listeners. 

## What is Flutter Sound?

Flutter Sound is a Flutter plugin that allows developers to record and play audio in their Flutter applications. It provides a simple and straightforward API for audio recording, playback, and manipulation. Flutter Sound supports various audio features including audio encoding, decibel level monitoring, and now we can also apply audio noise suppression.

## Adding Flutter Sound to your project

To get started, we need to add the Flutter Sound package to our Flutter project. Open your `pubspec.yaml` file and add the following dependency:

```dart
dependencies:
  flutter_sound: ^X.X.X
```

Replace `X.X.X` with the version you want to use, ensure to always use the latest stable version.

Once you have added the dependency, run `flutter pub get` to fetch the package.

## Implementing audio noise suppression

To implement audio noise suppression, we need to follow these steps:

### 1. Import the necessary packages

```dart
import 'package:flutter_sound/flutter_sound.dart' as sound;
import 'package:flutter_sound/noise_suppression.dart'; // Import the noise suppression package
```

### 2. Create an instance of the `FlutterSoundPlayer` and `FlutterSoundRecorder`

```dart
final sound.FlutterSoundPlayer _player = sound.FlutterSoundPlayer();
final sound.FlutterSoundRecorder _recorder = sound.FlutterSoundRecorder();
```

### 3. Enable noise suppression

```dart
await _recorder.openAudioSession();

// Enable noise suppression
await sound.FlutterSoundNoiseSuppressor.enable();
```

### 4. Start recording

To start recording, use the following code:

```dart
await _recorder.startRecorder(toFile: 'path_to_save/audio_file.aac', codec: sound.Codec.aacADTS);
```

### 5. Play the recorded audio

```dart
await _player.openAudioSession(); 

await _player.startPlayer(fromURI: 'path_to_saved/audio_file.aac');
```

### 6. Disable noise suppression

After you have finished recording or playing audio, don't forget to disable noise suppression:

```dart
// Disable noise suppression
await sound.FlutterSoundNoiseSuppressor.disable();
```

## Conclusion

In this blog post, we have learned how to implement audio noise suppression in a Flutter application using the Flutter Sound package. With just a few simple steps, we were able to enable noise suppression, record audio, and play it back with reduced background noise. Incorporating audio noise suppression can greatly enhance the audio experience for your users, providing a cleaner and clearer sound.
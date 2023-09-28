---
layout: post
title: "Implementing audio recording with Flutter Sound"
description: " "
date: 2023-09-25
tags: [audio]
comments: true
share: true
---

![flutter_sound](https://www.example.com/flutter_sound.jpg)

With Flutter Sound, you can easily add audio recording functionality to your Flutter applications. Whether you want to build a voice recorder, a podcast app, or any other application that requires audio recording, Flutter Sound has got you covered. In this blog post, we will walk you through the steps of implementing audio recording with Flutter Sound.

## Installing Flutter Sound

To get started, you need to add the Flutter Sound dependency to your `pubspec.yaml` file.
```yaml
dependencies:
  flutter_sound: ^2.0.2
```
Then, run `flutter pub get` to fetch the package.

## Recording an audio

To begin recording audio, you need to create an instance of the `FlutterSoundRecorder` class.
```dart
import 'package:flutter_sound/flutter_sound.dart';

FlutterSoundRecorder recorder = FlutterSoundRecorder();
```

Before recording, you should request audio recording permissions from the user. You can use the `hasPermission()` method to check if the permissions are already granted, and `openAudioSession()` method to request permissions if needed.
```dart
import 'package:flutter_sound/flutter_sound.dart';
import 'package:flutter_sound/android_encoder.dart' show AndroidEncoder;
import 'package:flutter_sound/ios_quality.dart' show IosQuality;

FlutterSoundRecorder recorder = FlutterSoundRecorder();
await recorder.openAudioSession(
  focus: AudioFocus.requestFocusTransient,
  category: SessionCategory.record,
  androidEncoder: AndroidEncoder.AAC,
  iosQuality: IosQuality.LOW,
);
```

Start recording by calling the `startRecorder()` method on the `recorder` instance.
```dart
recorder.startRecorder(toFile: filename);
```

Stop recording using the `stopRecorder()` method.
```dart
recorder.stopRecorder();
```

## Playing the recorded audio

To play the recorded audio, create an instance of the `FlutterSoundPlayer` class.
```dart
import 'package:flutter_sound/flutter_sound.dart';

FlutterSoundPlayer player = FlutterSoundPlayer();
```

Open the audio session for playing.
```dart
await player.openAudioSession();
```

Start playing the recorded audio file by calling the `startPlayer()` method.
```dart
player.startPlayer(fromURI: filename);
```

Stop the audio playback using the `stopPlayer()` method.
```dart
player.stopPlayer();
```

## Conclusion

In this blog post, we have learned how to implement audio recording in Flutter using the Flutter Sound library. With just a few steps, you can easily record and play audio in your Flutter applications. Flutter Sound provides additional features for modifying the audio, handling audio playback events, and more. To explore more about Flutter Sound, refer to the official documentation.

#flutter #audio-recording
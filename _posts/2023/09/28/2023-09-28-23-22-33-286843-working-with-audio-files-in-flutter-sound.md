---
layout: post
title: "Working with audio files in Flutter Sound"
description: " "
date: 2023-09-28
tags: [audio]
comments: true
share: true
---

Flutter Sound is a powerful audio library that allows developers to work with audio files in Flutter applications. Whether you need to play audio files, record audio, or apply various audio effects, Flutter Sound provides a simple and efficient way to accomplish these tasks.

In this article, we will explore how to work with audio files in Flutter Sound and cover some essential features and functionalities offered by this library.

## Installation

To get started with Flutter Sound, you need to add the library as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_sound: ^2.0.0
```

Then, run `flutter pub get` to fetch the library and its dependencies.

## Playing audio files

To play audio files in Flutter Sound, you can use the `FlutterSoundPlayer` class. Here's an example code snippet that demonstrates how to play an audio file:

```dart
import 'package:flutter_sound/flutter_sound.dart';

FlutterSoundPlayer _player = FlutterSoundPlayer();

void playAudio() async {
  await _player.openAudioSession();
  await _player.startPlayer(
    fromURI: 'path_to_audio_file.mp3',
    whenFinished: () => print('Playback finished'),
  );
}

void stopAudio() async {
  await _player.stopPlayer();
  await _player.closeAudioSession();
}
```

In the above code, we first create an instance of `FlutterSoundPlayer` and then open an audio session. We then start the player by providing the path to the audio file we want to play. You can also add a callback function to the `whenFinished` parameter to perform actions when the playback finishes.

To stop the audio playback, you can call the `stopPlayer()` method, and finally, don't forget to close the audio session using the `closeAudioSession()` method.

## Recording audio

Flutter Sound also provides functionality for recording audio using the `FlutterSoundRecorder` class. Here's an example of how to record audio:

```dart
import 'package:flutter_sound/flutter_sound.dart';

FlutterSoundRecorder _recorder = FlutterSoundRecorder();

void startRecording() async {
  await _recorder.openAudioSession();
  await _recorder.startRecorder(
    toFile: 'path_to_output_file.mp3',
  );
}

void stopRecording() async {
  await _recorder.stopRecorder();
  await _recorder.closeAudioSession();
}
```

In the code snippet above, we create an instance of `FlutterSoundRecorder` and open an audio session. We then start the recorder and provide the path where we want to save the recorded audio. To stop the recording, simply call the `stopRecorder()` method, and close the audio session using the `closeAudioSession()` method.

## Applying audio effects

Flutter Sound allows you to apply various audio effects to the recorded or playing audio files. It provides a set of predefined effects that you can use. Here's an example of how to apply an audio effect:

```dart
import 'package:flutter_sound/flutter_sound.dart';

FlutterSoundPlayer _player = FlutterSoundPlayer();

void applyEffect() async {
  await _player.openAudioSession();
  await _player.setVolume(0.5);
  await _player.setSpeed(1.5);
  await _player.setPitch(0.8);
}

void stopEffect() async {
  await _player.stopPlayer();
  await _player.closeAudioSession();
}
```

In the above code, we apply three different effects: volume, speed, and pitch. By calling the respective methods, we can adjust the volume, increase or decrease the playback speed, and change the pitch of the audio file.

## Conclusion

Working with audio files in Flutter Sound is straightforward and offers a range of features and functionalities. Whether you need to play audio files, record audio, or apply audio effects, Flutter Sound provides the necessary tools to accomplish these tasks with ease.

Make sure to explore the official documentation for further details on all the available features and options provided by Flutter Sound.

#flutter #audio
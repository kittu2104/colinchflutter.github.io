---
layout: post
title: "Integrating audio background playback with Flutter Sound"
description: " "
date: 2023-09-25
tags: [audio]
comments: true
share: true
---

In this blog post, we will explore how to integrate audio background playback with Flutter Sound. Flutter Sound is a powerful audio recording and playback library for Flutter applications.

## Why background playback?

Background playback allows users to listen to audio even when they switch to other apps or lock their devices. This functionality is crucial for media applications, such as music players or podcast players, as it enhances user experience and convenience.

## Getting started with Flutter Sound

Before we dive into the integration, make sure you have Flutter Sound set up in your Flutter project. You can add it as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_sound: ^x.x.x
```

Replace `x.x.x` with the latest version of Flutter Sound.

## Setting up audio service

To achieve background playback, we will use a package called audio_service. This package provides a unified API for background audio playback on both Android and iOS.

Add audio_service to your `pubspec.yaml` file:

```yaml
dependencies:
  audio_service: ^x.x.x
```

Now, create a new Dart file, `audio_player.dart`, in your project directory, and import the necessary packages:

```dart
import 'package:audio_service/audio_service.dart';
import 'package:flutter_sound/flutter_sound.dart';
```

Next, create a class called `AudioPlayer` that extends `BackgroundAudioTask` from audio_service:

```dart
class AudioPlayer extends BackgroundAudioTask {
  FlutterSoundPlayer _player = FlutterSoundPlayer();

  // Implementation goes here
}
```

## Implementing background playback

Inside the `AudioPlayer` class, we will implement the necessary methods to handle background audio playback:

### `onStart`

The `onStart` method is called when the audio playback is initiated. Here, we will configure the audio playback settings and start playing the audio:

```dart
@override
Future<void> onStart() async {
  await _player.openAudioSession();
  await _player.startPlayer(
    fromURI: 'https://example.com/audio.mp3',
    codec: Codec.mp3,
  );
}
```

Make sure to replace the example URL with the actual URL of the audio file you want to play.

### `onStop`

The `onStop` method is called when the audio playback is stopped. Here, we will stop the player and release the audio session:

```dart
@override
Future<void> onStop() async {
  await _player.stopPlayer();
  await _player.closeAudioSession();
  super.onStop();
}
```

### `onPlay`

The `onPlay` method is called when the audio playback is resumed. Here, we will resume playing the audio:

```dart
@override
Future<void> onPlay() async {
  await _player.resumePlayer();
  super.onPlay();
}
```

### `onPause`

The `onPause` method is called when the audio playback is paused. Here, we will pause the player:

```dart
@override
Future<void> onPause() async {
  await _player.pausePlayer();
  super.onPause();
}
```

### `onTaskRemoved`

The `onTaskRemoved` method is called when the task is removed from the operating system's tasks list. Here, we will stop the player:

```dart
@override
void onTaskRemoved() {
  _player.stopPlayer();
  _player.closeAudioSession();
  super.onTaskRemoved();
}
```

## Registering the audio player

Finally, we need to register our `AudioPlayer` class as the audio task in the `main()` function of our Flutter app:

```dart
void main() {
  AudioServiceBackground.run(() => AudioPlayer());
}
```

## Conclusion

In this blog post, we learned how to integrate background audio playback with Flutter Sound using the audio_service package. With this integration, your Flutter app can provide a seamless audio experience, even when the app is running in the background or the device is locked.

Now it's time to take your Flutter audio app to the next level and provide an uninterrupted audio experience for your users!

#flutter #audio #backgroundplayback
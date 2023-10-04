---
layout: post
title: "Implementing audio equalization presets with Flutter Sound"
description: " "
date: 2023-09-28
tags: [audioequalization]
comments: true
share: true
---

If you are building an audio player or a music app using Flutter Sound, you may want to provide your users with audio equalization presets. These presets allow users to enhance the sound according to their preferences or the genre of music they are listening to. In this blog post, we will explore how to implement audio equalization presets using the Flutter Sound library.

## What is Flutter Sound?

Flutter Sound is a powerful audio player and recorder plugin for Flutter apps. It offers a wide range of features for audio playback, recording, and manipulation. You can use Flutter Sound to play local audio files, stream audio from URLs, record audio, apply audio effects, and much more.

## Adding Audio Equalization Presets

To implement audio equalization presets with Flutter Sound, we need to use the Flutter audio_session package. This package provides an easy way to interact with the device's audio session, including audio equalization settings.

### 1. Add the audio_session package to your pubspec.yaml file:

```yaml
dependencies:
  flutter_sound: ^x.x.x
  audio_session: ^x.x.x
```

Make sure to replace `x.x.x` with the latest version numbers of the Flutter Sound and audio_session packages.

### 2. Request audio session:

Before applying equalization presets, we need to request an audio session with the necessary configuration. Add the following code to your Flutter Sound initialization or audio playback code:

```dart
import 'package:audio_session/audio_session.dart';

final session = await AudioSession.instance;
await session.configure(AudioSessionConfiguration.speech());

// You can replace AudioSessionConfiguration.speech() with other configurations as per your requirements.
```

### 3. Apply equalization preset:

Now that we have our audio session configured, we can apply equalization presets to the audio player. Flutter Sound provides the `setEqualizer` method to change the equalization settings. Here is an example of applying a preset:

```dart
import 'package:flutter_sound/flutter_sound.dart';

final flutterSound = FlutterSound();
await flutterSound.setEqualizer(FlutterSoundEqualizerPreset.pop);
```

You can replace `FlutterSoundEqualizerPreset.pop` with other presets like `FlutterSoundEqualizerPreset.rock` or `FlutterSoundEqualizerPreset.classical`, or even create custom equalizer settings by passing an array of frequency gains to the `setEqualizer` method.

### 4. Reset equalization settings:

If you want to reset the equalization settings to their default values, you can use the `resetEqualizer` method:

```dart
await flutterSound.resetEqualizer();
```

### 5. Dispose the audio session:

To clean up and release the audio session, don't forget to dispose of it when you are done using it:

```dart
await session.dispose();
```

## Conclusion

In this blog post, we have seen how to implement audio equalization presets using Flutter Sound. By integrating the audio_session package with Flutter Sound, we can easily configure and apply equalization settings to enhance the audio experience for our users. Experiment with different presets and custom equalizer settings to provide a personalized listening experience in your Flutter apps.

#flutter #audioequalization
---
layout: post
title: "Recording and playback of ambient sounds in a Flutter app"
description: " "
date: 2023-09-18
tags: [ambientSounds]
comments: true
share: true
---

In this blog post, we will explore how to implement recording and playback of ambient sounds in a Flutter app. This can be useful for various applications such as voice recording, audio memos, or sound effects playback.

## Setup

To begin, make sure you have Flutter installed on your machine. You can follow the official Flutter installation guide for instructions on how to set it up.

## Dependencies

We'll be using the `flutter_sound` package for recording and playback of sounds. Add the following line to your `pubspec.yaml` file to add the dependency:

```yaml
dependencies:
  flutter_sound: ^x.x.x
```

Make sure to replace `x.x.x` with the desired version of `flutter_sound`.

After adding the dependency, run `flutter pub get` to fetch the package.

## Recording

To record ambient sounds, we need to use the device's microphone. Flutter provides the `flutter_sound` package with all the necessary APIs for recording audio.

First, we need to request permission to use the microphone. Add the following code to your `AndroidManifest.xml` file within the `<manifest>` tag:

```xml
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

For iOS, open the `Info.plist` file and add the following key-value pair:

```xml
<key>NSMicrophoneUsageDescription</key>
<string>Microphone permission is required for audio recording</string>
```

Now we can start recording by initializing an instance of `FlutterSoundRecorder`. Use the following code to start recording:

```dart
import 'package:flutter_sound/flutter_sound.dart';

final recorder = FlutterSoundRecorder();

await recorder.openAudioSession();
await recorder.startRecorder(toFile: filePath);
```

Replace `filePath` with the desired location to save the recorded audio file.

## Playback

To play back the recorded audio, we can use the `FlutterSoundPlayer` class. Make sure to import the `flutter_sound/flutter_sound.dart` package.

To start playback, use the following code:

```dart
import 'package:flutter_sound/flutter_sound.dart';

final player = FlutterSoundPlayer();

await player.openAudioSession();
await player.startPlayer(fromURI: filePath);
```

Replace `filePath` with the location of the recorded audio file.

## Conclusion

In this blog post, we learned how to implement recording and playback of ambient sounds in a Flutter app using the `flutter_sound` package. We covered how to request microphone permissions, start recording, and play back the recorded audio. This functionality can be extended to build various audio-related features in your Flutter applications.

#flutter #ambientSounds
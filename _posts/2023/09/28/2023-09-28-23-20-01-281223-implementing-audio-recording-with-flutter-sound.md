---
layout: post
title: "Implementing audio recording with Flutter Sound"
description: " "
date: 2023-09-28
tags: [Flutter, AudioRecording]
comments: true
share: true
---

***Steps to Implement Audio Recording with Flutter Sound***

***1. Add Flutter Sound Dependency***
To get started, you need to add the Flutter Sound dependency to your project. Open your project's `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter_sound: ^x.x.x
```

Replace `^x.x.x` with the latest version of Flutter Sound.

***2. Requesting Permissions***
Before starting the audio recording, you need to request the necessary permissions from the user. Add the following code to your Dart file:

```dart
import 'package:permission_handler/permission_handler.dart';

// ...

Future<void> _checkPermission() async {
  final status = await Permission.microphone.request();
  if (status != PermissionStatus.granted) {
    throw Exception('Microphone permission not granted');
  }
}

```

Here we are using the `permission_handler` package to request microphone permissions from the user. Make sure to add this package to your `pubspec.yaml` file.

***3. Recording Audio***
Now let's implement the audio recording functionality. Add the following code to your Dart file:

```dart
import 'package:flutter_sound/flutter_sound.dart';

// ...

FlutterSoundPlayer _soundPlayer;
FlutterSoundRecorder _soundRecorder;

// ...

void _startRecording() async {
  await _checkPermission();

  _soundRecorder = FlutterSoundRecorder();

  await _soundRecorder.openAudioSession();
  await _soundRecorder.startRecorder(
    toFile: 'path_to_save_audio_file',
    codec: Codec.aacADTS,
  );
}

void _stopRecording() async {
  await _soundRecorder.stopRecorder();
  await _soundRecorder.closeAudioSession();
}
```

In the `_startRecording` method, we first check for microphone permissions by calling `_checkPermission`. If the permission is granted, we initialize the FlutterSoundRecorder and start the recording using the `startRecorder` method. Replace `'path_to_save_audio_file'` with the desired location to save the audio file on the device.

The `_stopRecording` method stops the recording by calling `stopRecorder` and closes the audio session.

***4. Playing Recorded Audio***
To play the recorded audio, add the following code:

```dart
void _startPlaying() async {
  _soundPlayer = FlutterSoundPlayer();

  await _soundPlayer.openAudioSession();
  await _soundPlayer.startPlayer(
    fromURI: 'path_to_audio_file',
    codec: Codec.aacADTS,
  );
}

void _stopPlaying() async {
  await _soundPlayer.stopPlayer();
  await _soundPlayer.closeAudioSession();
}
```

In the `_startPlaying` method, we initialize the FlutterSoundPlayer and start playing the audio using the `startPlayer` method. Replace `'path_to_audio_file'` with the location of the recorded audio file.

The `_stopPlaying` method stops the player by calling `stopPlayer` and closes the audio session.

***5. UI Integration***
Finally, integrate the audio recording and playback functionality into your user interface, such as buttons for starting and stopping the recording and playback.

```dart
ElevatedButton(
  onPressed: _startRecording,
  child: Text('Start Recording'),
),

ElevatedButton(
  onPressed: _stopRecording,
  child: Text('Stop Recording'),
),

ElevatedButton(
  onPressed: _startPlaying,
  child: Text('Start Playing'),
),

ElevatedButton(
  onPressed: _stopPlaying,
  child: Text('Stop Playing'),
),
```

***Conclusion***
In this tutorial, we explored how to implement audio recording using Flutter Sound. We covered the steps required to request microphone permissions, start and stop audio recording, and play the recorded audio. Flutter Sound provides a simple and powerful way to add audio recording capabilities to your Flutter applications.

Try out Flutter Sound in your next Flutter project and enhance the user experience with audio recording and playback!

**#Flutter** **#AudioRecording**
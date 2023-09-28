---
layout: post
title: "Implementing audio noise suppression with Flutter Sound"
description: " "
date: 2023-09-25
tags: [flutterSound]
comments: true
share: true
---

![Flutter Sound](https://flutter.dev/images/flutter-logo-sharing.png)

Audio noise can be a major disturbance when recording or playing back audio in mobile applications. Fortunately, Flutter provides a powerful audio plugin called Flutter Sound that allows us to implement noise suppression and enhance the audio quality.

In this tutorial, we will explore how to implement audio noise suppression using Flutter Sound in a Flutter application.

## Prerequisites

To follow along with this tutorial, you need:

- Flutter SDK installed on your machine
- Flutter Sound added as a dependency in your Flutter project

## Setting up the project

First, let's create a new Flutter project:

```dart
flutter create noise_suppression_example
cd noise_suppression_example
```

Next, open the `pubspec.yaml` file and add `flutter_sound` as a dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_sound: ^0.10.0
```

Save the file and run `flutter pub get` to download and configure the dependencies.

## Implementing audio noise suppression

Now, let's create a basic Flutter application to demonstrate the audio noise suppression feature.

In the `lib/main.dart` file, update the code as follows:

```dart
import 'dart:async';
import 'package:flutter/material.dart';
import 'package:flutter_sound/flutter_sound.dart';

void main() => runApp(NoiseSuppressionApp());

class NoiseSuppressionApp extends StatefulWidget {
  @override
  _NoiseSuppressionAppState createState() => _NoiseSuppressionAppState();
}

class _NoiseSuppressionAppState extends State<NoiseSuppressionApp> {
  FlutterSoundPlayer _audioPlayer = FlutterSoundPlayer();

  StreamSubscription? _playerSubscription;

  @override
  void initState() {
    super.initState();
    _initAudioPlayer();
  }

  Future<void> _initAudioPlayer() async {
    await _audioPlayer.openAudioSession();
    await _audioPlayer.setSubscriptionDuration(Duration(milliseconds: 10));
  }

  void _playAudioWithNoiseSuppression() async {
    await _audioPlayer.startPlayer(
      fromURI: 'path_to_audio_file',
      codec: Codec.aacADTS,
      withNoiseSuppression: true,
    );
    _playerSubscription = _audioPlayer.onProgress.listen((e) {
      // Handle audio progress updates here
    });
  }

  void _stopAudio() {
    _audioPlayer.stopPlayer();
    _playerSubscription?.cancel();
  }

  @override
  void dispose() {
    _audioPlayer.closeAudioSession();
    _audioPlayer = FlutterSoundPlayer();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Audio Noise Suppression'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              ElevatedButton(
                onPressed: _playAudioWithNoiseSuppression,
                child: Text('Play Audio with Noise Suppression'),
              ),
              ElevatedButton(
                onPressed: _stopAudio,
                child: Text('Stop Audio'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

In this code, we've created a `NoiseSuppressionApp` widget that initializes the `FlutterSoundPlayer` and sets up the audio player with noise suppression. On button presses, we call `_playAudioWithNoiseSuppression` to start playing audio with noise suppression enabled and `_stopAudio` to stop the audio playback.

Replace `'path_to_audio_file'` with the path to the audio file you want to play.

## Testing the application

To test the application, connect your mobile device or start an emulator, and run the following command:

```dart
flutter run
```

After a successful build, you should see the app running on your device/emulator. Press the "Play Audio with Noise Suppression" button to start playing the audio with noise suppression. Press the "Stop Audio" button to stop the audio playback.

Congratulations! You have successfully implemented audio noise suppression using Flutter Sound in your Flutter application.

## Conclusion

Audio noise suppression is crucial for providing a better audio experience in mobile applications. In this tutorial, we explored how to implement audio noise suppression using Flutter Sound. Now, you can enhance your audio playback or recording capabilities by incorporating noise suppression into your Flutter projects.

#flutter #flutterSound #audio #noiseSuppression
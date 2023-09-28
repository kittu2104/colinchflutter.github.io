---
layout: post
title: "Adding audio effects with Flutter Sound"
description: " "
date: 2023-09-28
tags: []
comments: true
share: true
---

If you're building a multimedia app with audio playback functionality, you may want to enhance the user experience by adding audio effects. Flutter Sound is a powerful audio plugin for Flutter that allows you to play, record, and process audio files. In this tutorial, we will learn how to use Flutter Sound to apply audio effects to the playback.

## Step 1: Setup Flutter Sound

First, make sure you have Flutter and Dart installed on your machine. Then, create a new Flutter project by running the following command:

```bash
flutter create audio_effects_app
```

Navigate to the project directory:

```bash
cd audio_effects_app
```

Open the `pubspec.yaml` file and add the `flutter_sound` dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_sound: ^x.x.x
```

Replace `x.x.x` with the latest version of `flutter_sound` plugin. Save the changes and run the following command to fetch the dependencies:

```bash
flutter pub get
```

## Step 2: Add Audio File

Locate or download an audio file that you want to apply effects to and add it to your project. You can place the audio file in the `assets` folder under the project's root directory.

## Step 3: Implement Flutter Sound

Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_sound/flutter_sound.dart';

void main() {
  runApp(MaterialApp(
    home: AudioEffectsApp(),
  ));
}

class AudioEffectsApp extends StatefulWidget {
  @override
  _AudioEffectsAppState createState() => _AudioEffectsAppState();
}

class _AudioEffectsAppState extends State<AudioEffectsApp> {
  FlutterSoundPlayer? _player;
  bool _isPlaying = false;

  @override
  void initState() {
    super.initState();
    _player = FlutterSoundPlayer();
  }

  Future<void> _playAudioWithEffects() async {
    await _player?.openAudio("assets/audio_file.mp3", mode: PlayerMode.MEDIA_PLAYER);
    await _player?.setVolume(1.0);
    await _player?.startPlayerFromBeginning();
    setState(() {
      _isPlaying = true;
    });
  }

  Future<void> _stopAudio() async {
    await _player?.stopPlayer();
    setState(() {
      _isPlaying = false;
    });
  }

  @override
  void dispose() {
    _player?.release();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Audio Effects App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: _isPlaying ? null : _playAudioWithEffects,
              child: Text('Play Audio with Effects'),
            ),
            SizedBox(height: 16),
            ElevatedButton(
              onPressed: _isPlaying ? _stopAudio : null,
              child: Text('Stop Audio'),
            ),
          ],
        ),
      ),
    );
  }
}
```

This code sets up a basic Flutter app with two buttons: one for playing the audio with effects and another for stopping the audio playback.

## Step 4: Apply Audio Effects

Flutter Sound provides a wide range of audio effects that you can apply to the audio playback. You can experiment with various effects such as pitch shift, reverb, equalization, and more. To apply an effect, use the `await _player?.setXXX()` methods before starting the player.

For example, to set the audio playback pitch to a higher value, add the following line before `await _player?.startPlayerFromBeginning()` in the `_playAudioWithEffects` function:

```dart
await _player?.setPitch(1.5);
```

Similarly, you can add other effects based on your requirements using the available methods in `flutter_sound` package.

## Step 5: Run the App

Save the changes, and run the app on your preferred device or emulator:

```bash
flutter run
```

You should now be able to play the audio file with the applied effects using the Flutter Sound plugin.

# Conclusion

In this tutorial, we learned how to enhance audio playback in a Flutter app by adding audio effects using the Flutter Sound plugin. You can explore the different audio effects provided by the plugin and experiment with them to provide a more immersive audio experience to your users. Happy coding!
---
layout: post
title: "Implementing audio spectrum analysis and visualization in a Flutter app"
description: " "
date: 2023-09-18
tags: [flutter, audioplayers]
comments: true
share: true
---

Flutter is a powerful framework for building cross-platform apps, and it offers a wide range of features and plugins for creating rich and interactive experiences. One popular use case is creating audio apps that involve audio spectrum analysis and visualization.

In this tutorial, we will explore how to implement audio spectrum analysis and visualization in a Flutter app using the audioplayers plugin and the Flutter Sound FFT package.

## Prerequisites

Before getting started, make sure you have Flutter and Dart installed on your machine. You can install them by following the official Flutter documentation.

## Setting up the project

Let's start by creating a new Flutter project with the following command:

```bash
flutter create audio_visualizer
```

Next, navigate into the project directory:

```bash
cd audio_visualizer
```

Open the `pubspec.yaml` file and add the `audioplayers` and `flutter_sound_fft` dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  audioplayers: ^0.19.1
  flutter_sound_fft: ^0.3.2
```

Save the file and run the following command to fetch the dependencies:

```bash
flutter pub get
```

## Implementing the audio player

In order to analyze and visualize the audio spectrum, we need to play an audio file. For this example, we will use the `audioplayers` plugin to handle audio playback.

Create a new Dart file called `audio_player.dart` and add the following code:

```dart
import 'package:audioplayers/audioplayers.dart';

class AudioPlayer {
  final audioPlayer = AudioPlayer();
  
  Future<void> play(String audioFilePath) async {
    await audioPlayer.play(audioFilePath, isLocal: true);
  }

  Future<void> pause() async {
    await audioPlayer.pause();
  }

  Future<int> getDuration() async {
    return await audioPlayer.getDuration();
  }

  Stream<AudioPlayerState> get playerStateStream =>
      audioPlayer.onPlayerStateChanged;
}
```

This class provides a simple interface to play audio files, pause the playback, and get the duration of the audio file. It also exposes a `playerStateStream` stream that we will use to listen to changes in the player state.

## Implementing the audio spectrum visualization

Now that we have our audio player set up, let's implement the audio spectrum visualization.

Create a new Dart file called `audio_visualizer.dart` and add the following code:

```dart
import 'dart:typed_data';

import 'package:flutter/material.dart';
import 'package:flutter_sound_fft/flutter_sound_fft.dart';

class AudioVisualizer extends StatefulWidget {
  final AudioPlayer audioPlayer;

  const AudioVisualizer({Key? key, required this.audioPlayer}) : super(key: key);

  @override
  _AudioVisualizerState createState() => _AudioVisualizerState();
}

class _AudioVisualizerState extends State<AudioVisualizer> {
  List<double> audioSamples = [];
  List<double> audioSpectrum = [];
  bool isPlaying = false;

  final FlutterSoundFft _fft = FlutterSoundFft();
  late StreamSubscription<AudioPlayerState> _audioPlayerStateSubscription;

  @override
  void initState() {
    super.initState();
    _audioPlayerStateSubscription =
        widget.audioPlayer.playerStateStream.listen((state) {
      setState(() {
        isPlaying = state == AudioPlayerState.PLAYING;
      });

      if (isPlaying) {
        _startSpectrumAnalysis();
      }
    });
  }

  Future<void> _startSpectrumAnalysis() async {
    _fft.init();
    final duration = await widget.audioPlayer.getDuration();

    while (isPlaying) {
      audioSamples =
          await _fft.audioStream.take(duration ~/ 1000).toList() as List<double>;
      audioSpectrum = _fft.getSpectrum(audioSamples);
      setState(() {});

      await Future.delayed(const Duration(milliseconds: 100));
    }
  }

  @override
  void dispose() {
    _fft.stop();
    _audioPlayerStateSubscription.cancel();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    // Build your audio spectrum visualization UI here
  }
}
```

This code sets up the audio spectrum visualization by initializing the Flutter Sound FFT package and listening to changes in the audio player's state. When the audio player starts playing, it starts analyzing the audio samples using `FlutterSoundFft`'s `getSpectrum` method and updates the UI accordingly.

## Building the UI

Now that we have our audio player and audio spectrum visualization set up, let's integrate them into the UI.

Open the `main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'audio_player.dart';
import 'audio_visualizer.dart';

void main() {
  runApp(AudioVisualizerApp());
}

class AudioVisualizerApp extends StatelessWidget {
  final AudioPlayer audioPlayer = AudioPlayer();

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Audio Visualizer App'),
        ),
        body: Column(
          children: [
            const SizedBox(height: 16),
            AudioVisualizer(audioPlayer: audioPlayer),
            const SizedBox(height: 16),
            ElevatedButton(
              onPressed: () {
                audioPlayer.play('path_to_audio_file.mp3');
              },
              child: const Text('Play'),
            ),
            ElevatedButton(
              onPressed: () {
                audioPlayer.pause();
              },
              child: const Text('Pause'),
            ),
          ],
        ),
      ),
    );
  }
}
```

This code sets up the main app widget, which includes the `AudioVisualizer` widget, audio player controls, and buttons to play and pause the audio.

## Conclusion

By following this tutorial, you have learned how to implement audio spectrum analysis and visualization in a Flutter app. You can now create your own audio apps with real-time audio spectrum visualizations. Experiment with different audio files and UI designs to create a unique and engaging experience for your users.

#flutter #audioplayers #audiovisualization
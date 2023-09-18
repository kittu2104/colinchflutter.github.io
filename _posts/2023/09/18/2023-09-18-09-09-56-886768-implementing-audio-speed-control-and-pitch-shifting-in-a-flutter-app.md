---
layout: post
title: "Implementing audio speed control and pitch shifting in a Flutter app"
description: " "
date: 2023-09-18
tags: [audioplayer]
comments: true
share: true
---

Flutter is a powerful framework for building cross-platform mobile apps, and it provides various plugins and packages that make it easy to implement advanced features. In this blog post, we will explore how to implement audio speed control and pitch shifting in a Flutter app using the `audioplayers` package.

## Setting Up the Project

To get started, create a new Flutter project and add the `audioplayers` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  audioplayers: ^0.19.0
```

Save the file and run the `flutter pub get` command to fetch the package.

## Playing Audio

To play audio in Flutter, we'll use the `audioplayers` package. First, import the package into your Dart file:

```dart
import 'package:audioplayers/audioplayers.dart';
```

Initialize the audio player:

```dart
AudioPlayer audioPlayer = AudioPlayer();
```

Load and play the audio file:

```dart
String audioPath = "assets/audio/sample.mp3";
int audioId = await audioPlayer.play(audioPath, isLocal: true);
```

## Controlling Speed and Pitch

To control the speed and pitch of the audio, we'll use the `setPlaybackRate` and `setPitch` methods provided by the `audioplayers` package.

To control the speed, you can use the `setPlaybackRate` method:

```dart
double speed = 2.0; // Increase the speed by 2x
await audioPlayer.setPlaybackRate(playbackRate: speed);
```

To control the pitch, you can use the `setPitch` method:

```dart
double pitch = 1.5; // Increase the pitch by 1.5x
await audioPlayer.setPitch(pitch);
```

You can experiment with different speed and pitch values to achieve the desired audio effect.

## Example Usage

Here's an example of how you can implement audio speed control and pitch shifting in a Flutter app:

```dart
import 'package:flutter/material.dart';
import 'package:audioplayers/audioplayers.dart';

class AudioPlayerScreen extends StatefulWidget {
  @override
  _AudioPlayerScreenState createState() => _AudioPlayerScreenState();
}

class _AudioPlayerScreenState extends State<AudioPlayerScreen> {
  AudioPlayer audioPlayer = AudioPlayer();
  double speed = 1.0;
  double pitch = 1.0;

  void playAudio() async {
    String audioPath = "assets/audio/sample.mp3";
    int audioId = await audioPlayer.play(audioPath, isLocal: true);
    // Set initial speed and pitch values
    await audioPlayer.setPlaybackRate(playbackRate: speed);
    await audioPlayer.setPitch(pitch);
  }

  void updateSpeed(double newSpeed) async {
    setState(() {
      speed = newSpeed;
    });
    await audioPlayer.setPlaybackRate(playbackRate: speed);
  }

  void updatePitch(double newPitch) async {
    setState(() {
      pitch = newPitch;
    });
    await audioPlayer.setPitch(pitch);
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Audio Player"),
      ),
      body: Column(
        children: [
          Slider(
            value: speed,
            min: 0.5,
            max: 2.0,
            onChanged: updateSpeed,
          ),
          Slider(
            value: pitch,
            min: 0.5,
            max: 2.0,
            onChanged: updatePitch,
          ),
          IconButton(
            icon: Icon(Icons.play_arrow),
            onPressed: playAudio,
          ),
        ],
      ),
    );
  }
}
```

In this example, we have implemented a simple audio player screen with sliders to control the speed and pitch of the audio. The `playAudio` method loads and plays the audio file, and the `updateSpeed` and `updatePitch` methods update the speed and pitch values when the sliders are moved.

## Conclusion

In this blog post, we learned how to implement audio speed control and pitch shifting in a Flutter app using the `audioplayers` package. With these features, you can enhance the user experience of your app by allowing users to control the playback speed and pitch of audio files. Have fun experimenting with different audio effects in your Flutter app!

#flutter #audioplayer
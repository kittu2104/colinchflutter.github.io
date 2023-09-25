---
layout: post
title: "Implementing an audio player in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [audioplayer]
comments: true
share: true
---

Flutter is a powerful framework for building cross-platform mobile applications. It provides a wide range of features and widgets that make developing apps a breeze. One common requirement in many apps is the need for an audio player to play audio files. In this guide, we will walk through how to implement an audio player in a StatelessWidget in Flutter.

## Step 1: Adding dependencies

To play audio files in Flutter, we need to include the [audioplayers](https://pub.dev/packages/audioplayers) package in our project. Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  audioplayers: ^0.19.1
```

Save the file and run `flutter packages get` in your terminal to fetch the package.

## Step 2: Creating a stateless widget

In Flutter, a `StatelessWidget` is a widget that does not change state over time. Since we only need to play audio without any dynamic changes, we can use a `StatelessWidget` for our audio player.

```dart
import 'package:flutter/material.dart';
import 'package:audioplayers/audioplayers.dart';

class AudioPlayerWidget extends StatelessWidget {
  final AudioPlayer audioPlayer = AudioPlayer();

  @override
  Widget build(BuildContext context) {
    return IconButton(
      icon: Icon(Icons.play_arrow),
      onPressed: _playAudio,
    );
  }

  void _playAudio() {
    String audioUrl = 'https://example.com/audio.mp3';
    audioPlayer.play(audioUrl);
  }
}
```

In the above code, we import the necessary packages and create an `AudioPlayer` instance. Inside the `build` method, we return an `IconButton` that triggers the `_playAudio` method when pressed. The `_playAudio` method takes a URL of the audio file and uses the `AudioPlayer` to play it.

## Step 3: Using the audio player widget

To use the `AudioPlayerWidget`, you can simply add it to your UI tree. For example, if you want to display the player in the app's main screen, add the following code:

```dart
import 'package:flutter/material.dart';
import 'audio_player_widget.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Audio Player'),
        ),
        body: Center(
          child: AudioPlayerWidget(),
        ),
      ),
    );
  }
}
```

In this code, we import the `AudioPlayerWidget`, create a `MyApp` class, and use the `AudioPlayerWidget` inside the `body` of the `Scaffold`.

## Conclusion

By following these steps, you can easily implement an audio player in a `StatelessWidget` in Flutter using the `audioplayers` package. This allows you to play audio files in your Flutter app with ease. Remember to handle any required permissions, error handling, and UI updates based on the player's state. Enjoy building your audio-enabled app using Flutter!

#flutter #audioplayer
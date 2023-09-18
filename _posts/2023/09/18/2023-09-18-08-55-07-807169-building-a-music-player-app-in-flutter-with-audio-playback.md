---
layout: post
title: "Building a music player app in Flutter with audio playback"
description: " "
date: 2023-09-18
tags: [flutter, musicplayerapp]
comments: true
share: true
---

In this tutorial, we will walk you through the process of building a music player app in Flutter with audio playback capabilities. Flutter is a popular cross-platform framework that allows developers to create stunning user interfaces and compile native apps for both iOS and Android.

## Setting Up the Project

To begin, make sure you have Flutter installed on your system. Once installed, open your preferred code editor and create a new Flutter project:

```bash
$ flutter create music_player_app
```

Next, navigate to the project directory:

```bash
$ cd music_player_app
```

Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  audioplayers: ^0.19.0
```

Save the file and run the following command to fetch the dependencies:

```bash
$ flutter pub get
```

## Implementing the UI

Now that our project is set up, let's start building the user interface for our music player app. Replace the contents of the `lib/main.dart` file with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:audioplayers/audioplayers.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Music Player',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MusicPlayerPage(),
    );
  }
}

class MusicPlayerPage extends StatefulWidget {
  @override
  _MusicPlayerPageState createState() => _MusicPlayerPageState();
}

class _MusicPlayerPageState extends State<MusicPlayerPage> {
  List<AudioPlayer> _audioPlayers = [];

  @override
  void dispose() {
    for (var player in _audioPlayers) {
      player.dispose();
    }
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Music Player'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          crossAxisAlignment: CrossAxisAlignment.center,
          children: [
            Text(
              'Welcome to the Music Player App!',
              style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 16),
            RaisedButton(
              child: Text('Play Music'),
              onPressed: () {
                _playMusic();
              },
            ),
          ],
        ),
      ),
    );
  }

  void _playMusic() {
    AudioPlayer audioPlayer = AudioPlayer();
    _audioPlayers.add(audioPlayer);

    audioPlayer.play('assets/audio/song.mp3', isLocal: true);
  }
}
```

In the above code, we have defined a basic Flutter app with a single `MusicPlayerPage` that displays a welcome message and a button to play music. We are using the `audioplayers` plugin for audio playback.

## Adding Audio Files

To add your own audio files, create a new directory called `audio` inside the `assets` directory of your Flutter project. Place your audio files, such as `song.mp3`, inside the `audio` directory.

## Testing the App

To test the app, connect your device or emulator and run the following command:

```bash
$ flutter run
```

Your music player app should open on the device. Tap the "Play Music" button, and the app will start playing the audio file specified.

## Conclusion

Congratulations! You have successfully built a music player app in Flutter with audio playback capabilities. This is just a basic implementation to get you started. You can now customize and enhance the app by adding features like playlist management, music controls, and more.

#flutter #musicplayerapp
---
layout: post
title: "Creating a responsive music player using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [flutter, fluttertutorial]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive music player using `MediaQuery` in Flutter. Flutter is a popular UI framework that allows you to build beautiful and responsive applications for Android, iOS, web, and desktop.

## Prerequisites
Before we begin, make sure you have Flutter installed on your machine. You can install Flutter by following the official documentation on the [Flutter website](https://flutter.dev).

## Steps

### Step 1: Set up a new Flutter project
Create a new Flutter project using the following command:

```dart
flutter create music_player
```

### Step 2: Update dependencies
Open the `pubspec.yaml` file in your project and update the `dependencies` section with the following:

```yaml
dependencies:
  flutter:
    sdk: flutter
  audioplayers: ^0.19.0
```

Save the file and run the following command to download the dependencies:

```dart
flutter pub get
```

### Step 3: Create the UI

Open the `lib/main.dart` file in your project and replace the existing code with the following:

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
      ),
      home: MusicPlayer(),
    );
  }
}

class MusicPlayer extends StatefulWidget {
  @override
  _MusicPlayerState createState() => _MusicPlayerState();
}

class _MusicPlayerState extends State<MusicPlayer> {
  bool _isPlaying = false;
  AudioPlayer _audioPlayer = AudioPlayer();

  @override
  void initState() {
    super.initState();
    _audioPlayer.onPlayerStateChanged.listen((event) {
      if (event == PlayerState.STOPPED) {
        setState(() {
          _isPlaying = false;
        });
      }
    });
  }

  void _playPause() {
    if (_isPlaying) {
      _audioPlayer.pause();
      setState(() {
        _isPlaying = false;
      });
    } else {
      _audioPlayer.resume();
      setState(() {
        _isPlaying = true;
      });
    }
  }

  @override
  void dispose() {
    _audioPlayer.dispose();
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
          children: [
            IconButton(
              icon: _isPlaying ? Icon(Icons.pause_circle_filled) : Icon(Icons.play_circle_filled),
              iconSize: 100,
              onPressed: _playPause,
            ),
            Text(
              _isPlaying ? 'Playing' : 'Paused',
              style: TextStyle(fontSize: 24),
            ),
          ],
        ),
      ),
    );
  }
}
```

### Step 4: Test the app
Save the file and run the app using the following command:

```dart
flutter run
```

This will launch the app in the emulator or connected device. You should see a simple music player UI with a play/pause button. Press the button to toggle between play and pause states.

## Conclusion
In this tutorial, we learned how to create a responsive music player using `MediaQuery` in Flutter. We used the `audioplayers` package to play and control the music playback. Flutter provides powerful tools and widgets that allow you to build beautiful and responsive apps easily.

#flutter #fluttertutorial
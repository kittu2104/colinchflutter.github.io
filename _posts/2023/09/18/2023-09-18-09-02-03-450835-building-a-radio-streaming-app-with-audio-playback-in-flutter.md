---
layout: post
title: "Building a radio streaming app with audio playback in Flutter"
description: " "
date: 2023-09-18
tags: [Flutter, RadioStreamingApp]
comments: true
share: true
---

In this blog post, we will explore how to build a radio streaming app with audio playback using Flutter, a cross-platform development framework. With the popularity of audio streaming services on mobile devices, having a radio streaming app can be a great addition to your app portfolio.

## Prerequisites
To follow along with this tutorial, you will need the following prerequisites:
- [Flutter SDK](https://flutter.dev) installed on your machine
- Basic knowledge of Flutter and Dart programming language

## Step 1: Setup Flutter Project
First, let's create a new Flutter project by running the following command in your terminal:
\```bash
flutter create radio_app
cd radio_app
\```

## Step 2: Add Dependencies
We need to add dependencies to our `pubspec.yaml` file. Open the file and add the following lines under the `dependencies` section:
\```yaml
dependencies:
  just_audio: ^0.4.3
  audio_service: ^0.16.3
  flutter_radio_player: ^1.2.1
\```

Save the file and run `flutter pub get` to fetch the added dependencies.

## Step 3: Building the UI
Now, let's build the user interface for our radio streaming app. Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(RadioApp());
}

class RadioApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Radio App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Radio App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Icon(Icons.radio, size: 100),
            SizedBox(height: 20),
            Text('Radio Station Name', style: TextStyle(fontSize: 20)),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                // Play/Pause logic goes here
              },
              child: Text('Play'),
            ),
          ],
        ),
      ),
    );
  }
}
```

This code creates a basic **MaterialApp** with an **AppBar** and a **Column** for our radio station name, play button, and radio icon.

## Step 4: Implementing Audio Playback

To handle audio playback, we will be using the **just_audio** and **audio_service** plugins. Create a new file called `radio_service.dart` in the `lib` directory and add the following code:

```dart
import 'package:audio_service/audio_service.dart';
import 'package:just_audio/just_audio.dart';

class RadioPlayerTask extends BackgroundAudioTask {
  AudioPlayer _audioPlayer = AudioPlayer();

  @override
  Future<void> onPlay() async {
    await _audioPlayer.setUrl('https://example.com/stream.mp3');
    _audioPlayer.play();
    AudioServiceBackground.setState(playing: true);
  }

  @override
  Future<void> onStop() async {
    _audioPlayer.stop();
    await _audioPlayer.dispose();
    AudioServiceBackground.setState(playing: false);
  }
}

void startRadioService() {
  AudioServiceBackground.run(() => RadioPlayerTask());
}
```

This code sets up the `RadioPlayerTask` class that will handle audio playback. We define the `onPlay` and `onStop` methods to control the audio player. The `startRadioService` function is used to initiate the background audio service.

## Step 5: Wiring It All Together

In the `lib/main.dart` file, replace the existing `HomePage` class with this updated code:

```dart
import 'package:flutter/material.dart';
import 'package:audio_service/audio_service.dart';

void main() {
  AudioServiceBackground.run(() => RadioPlayerTask());
  runApp(RadioApp());
}

class RadioApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Radio App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Radio App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Icon(Icons.radio, size: 100),
            SizedBox(height: 20),
            Text('Radio Station Name', style: TextStyle(fontSize: 20)),
            SizedBox(height: 20),
            StreamBuilder<bool>(
              stream: AudioService.playbackStateStream.map((state) => state.playing).distinct(),
              builder: (context, snapshot) {
                final playing = snapshot.data ?? false;
                return ElevatedButton(
                  onPressed: () {
                    if (playing) {
                      AudioService.stop();
                    } else {
                      AudioService.start(backgroundTaskEntrypoint: 'radio_service.dart');
                    }
                  },
                  child: Text(playing ? 'Pause' : 'Play'),
                );
              },
            ),
          ],
        ),
      ),
    );
  }
}
```

Here, we have updated the main function to start the radio service in the background using `AudioServiceBackground.run()`.

## Step 6: Testing the App

To test the app, run the following command in your terminal:
\```bash
flutter run
\```

You should see the radio streaming app running on your device or emulator. Tapping the "Play" button should start streaming the audio, and tapping it again should pause the audio playback.

# Conclusion

In this blog post, we learned how to build a radio streaming app with audio playback in Flutter. We covered the basic setup, implementing the UI, and controlling audio playback using background audio tasks. Feel free to further enhance the app with additional features like volume control or displaying metadata for the playing audio stream. Have fun building your radio streaming app!

\#Flutter #RadioStreamingApp
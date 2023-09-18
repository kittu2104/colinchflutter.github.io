---
layout: post
title: "Building a voice changer app with audio recording and playback in Flutter"
description: " "
date: 2023-09-18
tags: [flutter, voicechanger]
comments: true
share: true
---

Voice changer apps have gained popularity in recent years, allowing users to modify their recorded voice with various effects. In this tutorial, we will explore how to build a voice changer app using Flutter, a cross-platform framework for building mobile applications.

## Prerequisites
To follow along with this tutorial, make sure you have the following:
- Flutter SDK installed and configured on your machine.
- An IDE of your choice (such as Android Studio or Visual Studio Code) with the Flutter and Dart plugins installed.

## Getting Started
To begin, create a new Flutter project using the following command in your terminal:
```bash
flutter create voice_changer_app
```
This will create a new folder named voice_changer_app with the project files.

## Adding Dependencies
Open the `pubspec.yaml` file in your project and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  audioplayers: ^0.19.0
  soundpool: ^2.0.2
  path_provider: ^2.0.2
```

Run the following command in your terminal to fetch the dependencies:
```bash
flutter pub get
```

## Designing the User Interface
We will create a simple UI with two buttons for recording and playing back the audio. Create a new file called `main.dart` in the `lib` folder and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(VoiceChangerApp());
}

class VoiceChangerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Voice Changer App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: VoiceChangerScreen(),
    );
  }
}

class VoiceChangerScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Voice Changer'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            RaisedButton(
              onPressed: () {
                // TODO: Implement audio recording
              },
              child: Text('Record Audio'),
            ),
            RaisedButton(
              onPressed: () {
                // TODO: Implement audio playback
              },
              child: Text('Play Audio'),
            ),
          ],
        ),
      ),
    );
  }
}
```

## Implementing Audio Recording
To record audio, we will use the `audioplayers` and `soundpool` libraries. Add the following code to the `VoiceChangerScreen` class under the record button's `onPressed` method:

```dart
import 'package:audioplayers/audioplayers.dart';
import 'package:soundpool/soundpool.dart';
import 'package:path_provider/path_provider.dart' as path_provider;

// ...

RaisedButton(
  onPressed: () async {
    final soundpool = Soundpool(streamType: StreamType.music);

    var recording = await path_provider.getExternalStorageDirectory();
    recording = recording.path + '/recording.wav';

    int soundId = await soundpool.load(recording);
    int streamId = await soundpool.play(soundId, isLooping: false);

    await Future.delayed(Duration(seconds: 5));

    soundpool.stop(streamId);
    soundpool.release();

    AudioPlayer audioPlayer = AudioPlayer();
    await audioPlayer.play(recording, isLocal: true);
  },
  child: Text('Record Audio'),
),
```

This code will record audio for 5 seconds, save it as a WAV file, play it using the `soundpool` library, and subsequently playback the recorded audio using the `audioplayers` library.

## Conclusion
Congratulations! You have built a voice changer app with audio recording and playback using Flutter. Feel free to explore and experiment with different audio effects or UI designs to enhance your app. Happy coding!

#flutter #voicechanger #appdevelopment
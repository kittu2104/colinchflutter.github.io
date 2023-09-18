---
layout: post
title: "Recording and playback of environmental sounds in a Flutter application"
description: " "
date: 2023-09-18
tags: [audio]
comments: true
share: true
---

In this blog post, we will explore the process of recording and playing back environmental sounds in a Flutter application. We will use the built-in audio recording and playback capabilities provided by the Flutter SDK to achieve this functionality. Let's dive in!

## 1. Setting Up the Project

First, we need to set up a new Flutter project. Open a terminal or command prompt and run the following command:

```shell
flutter create environmental_sounds_app
```

This will create a new Flutter project named "environmental_sounds_app".

## 2. Adding Dependencies

To enable audio recording and playback, we need to add the "audioplayers" package to our project. Open the `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  audioplayers: ^0.20.1
```

Save the file and run the following command in the terminal to fetch the dependencies:

```shell
flutter pub get
```

## 3. Recording Environmental Sounds

To record environmental sounds, we need to set up a recording session. Let's create a new file named `sound_recorder.dart` and add the following code:

```dart
import 'package:audioplayers/audioplayers.dart';

Future<String> startRecording() async {
  AudioPlayer audioPlayer = AudioPlayer();
  String filePath = "path_to_save_recorded_sound.wav";
  await audioPlayer.startRecorder(toFile: filePath, audioOutputFormat: AudioOutputFormat.WAV);
  return filePath;
}

void stopRecording() {
  AudioPlayer audioPlayer = AudioPlayer();
  audioPlayer.stopRecorder();
}
```

This code sets up a recording session using the `startRecorder` method provided by the `AudioPlayer` class. It starts recording audio and saves the recorded sound to a file specified by the `filePath` variable. The `stopRecording` method stops the recording session.

## 4. Playback of Recorded Sounds

To play back the recorded sounds, let's create a new file named `sound_player.dart` and add the following code:

```dart
import 'package:audioplayers/audioplayers.dart';

void playSound(String filePath) {
  AudioPlayer audioPlayer = AudioPlayer();
  audioPlayer.play(filePath, isLocal: true);
}

void stopSound() {
  AudioPlayer audioPlayer = AudioPlayer();
  audioPlayer.stop();
}
```

The `playSound` method plays the sound file specified by the `filePath` parameter, and the `stopSound` method stops the playback session.

## 5. Integrating into the Flutter UI

Finally, let's integrate the sound recording and playback functionality into our Flutter UI. Open the `main.dart` file and modify the `build` method as follows:

```dart
import 'package:flutter/material.dart';
import 'sound_recorder.dart';
import 'sound_player.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Environmental Sounds App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: SoundScreen(),
    );
  }
}

class SoundScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Environmental Sounds'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            RaisedButton(
              child: Text('Start Recording'),
              onPressed: () {
                startRecording();
              },
            ),
            RaisedButton(
              child: Text('Stop Recording'),
              onPressed: () {
                stopRecording();
              },
            ),
            RaisedButton(
              child: Text('Play Sound'),
              onPressed: () {
                playSound('path_to_saved_sound.wav');
              },
            ),
            RaisedButton(
              child: Text('Stop Sound'),
              onPressed: () {
                stopSound();
              },
            ),
          ],
        ),
      ),
    );
  }
}
```

This code sets up a basic Flutter UI with buttons to start recording, stop recording, play the recorded sound, and stop the sound playback.

## Conclusion

In this blog post, we learned how to record and play back environmental sounds in a Flutter application. We used the "audioplayers" package to enable audio recording and playback, and integrated the functionality into a Flutter UI. Feel free to explore further and add more features to your environmental sounds app. Happy coding!

#flutter #audio #soundrecording #soundplayback
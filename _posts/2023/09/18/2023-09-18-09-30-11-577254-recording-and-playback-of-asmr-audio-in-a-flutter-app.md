---
layout: post
title: "Recording and playback of ASMR audio in a Flutter app"
description: " "
date: 2023-09-18
tags: [flutter, asmr]
comments: true
share: true
---

ASMR (Autonomous Sensory Meridian Response) is gaining popularity as a way to relax and reduce stress. Many people enjoy listening to ASMR audio recordings, but wouldn't it be great if you could record and play back your own ASMR sounds in a Flutter app? In this blog post, we'll explore how you can implement recording and playback of ASMR audio in a Flutter app.

## Creating the User Interface

First, let's start by creating the user interface for our app. We'll have two buttons, one for recording and another for playback. We'll also display the recorded audio waveform for a better user experience.

```dart
import 'package:flutter/material.dart';

class ASMRApp extends StatefulWidget {
  @override
  _ASMRAppState createState() => _ASMRAppState();
}

class _ASMRAppState extends State<ASMRApp> {
  bool isRecording = false;
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('ASMR App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            IconButton(
              onPressed: () {
                // TODO: Handle recording logic
              },
              icon: Icon(isRecording ? Icons.stop : Icons.mic),
            ),
            IconButton(
              onPressed: () {
                // TODO: Handle playback logic
              },
              icon: Icon(Icons.play_arrow),
            ),
            // TODO: Display audio waveform
          ],
        ),
      ),
    );
  }
}
```

## Recording Audio

To record audio in Flutter, we can use the `audioplayers` package. It provides a simple interface to record audio from the device's microphone. To add the package to your project, add the following dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  audioplayers: ^0.20.1
```

Once you've added the dependency, you can start recording audio in your app. Add the following code inside the `onPressed` callback of the record `IconButton`:

```dart
import 'package:audioplayers/audioplayers.dart';

final audioPlayer = AudioPlayer();

void _startRecording() async {
  await audioPlayer.startRecorder();
  setState(() {
    isRecording = true;
  });
}

void _stopRecording() async {
  await audioPlayer.stopRecorder();
  setState(() {
    isRecording = false;
  });
}
```

## Playback Audio

To play back the recorded audio, we'll use the same `audioplayers` package. Update the playback `IconButton` with the following code:

```dart
void _playAudio() async {
  await audioPlayer.play(audioPath, isLocal: true);
}

void _pauseAudio() async {
  await audioPlayer.pause();
}

void _stopAudio() async {
  await audioPlayer.stop();
}
```

Make sure to replace `audioPath` with the actual path of the recorded audio file.

## Displaying Audio Waveform

To display the audio waveform, we can use the `waves` package. It allows us to visualize audio data as a waveform. To add the package to your project, add the following dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  waves: ^0.1.4
```

Once added, import the package and create a `WaveScreen` widget in your user interface:

```dart
import 'package:waves/waves.dart';

class WaveScreen extends StatelessWidget {
  final List<double> audioData;
  
  const WaveScreen({Key? key, required this.audioData}) : super(key: key);
  
  @override
  Widget build(BuildContext context) {
    return Container(
      height: 100,
      child: WaveWidget(
        audioData: audioData,
        // Customize waveform appearance if needed
      ),
    );
  }
}
```

Now, you can pass the recorded audio data to the `WaveScreen` widget and display the waveform in your app.

## Conclusion

In this blog post, we explored how to implement recording and playback of ASMR audio in a Flutter app. We created a user interface with buttons for recording and playback, displayed the audio waveform, and used the `audioplayers` and `waves` packages to handle recording and playback of audio. With this implementation, you can now create your own ASMR app and enjoy the soothing sounds of ASMR anytime, anywhere.

#flutter #asmr #audioplayback #flutterapp #waves
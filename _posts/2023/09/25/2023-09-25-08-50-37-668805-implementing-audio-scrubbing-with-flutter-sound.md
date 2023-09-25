---
layout: post
title: "Implementing audio scrubbing with Flutter Sound"
description: " "
date: 2023-09-25
tags: [flutter, flutter_sound]
comments: true
share: true
---

## Getting Started

Before we dive into the implementation details, make sure you have Flutter and the Flutter Sound package installed in your project.

```dart
dependencies:
  flutter_sound: ^x.x.x
```

Replace `x.x.x` with the latest version of the Flutter Sound package.

## Audio Scrubbing Widget

To create an audio scrubbing widget, we will use the `flutter_slider` package for the progress bar and Flutter Sound functions for controlling the audio playback.

Start by importing the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_slider/flutter_slider.dart';
import 'package:flutter_sound/flutter_sound.dart';
```

Next, create a class for the audio scrubbing widget:

```dart
class AudioScrubber extends StatefulWidget {
  final String audioPath;

  AudioScrubber({required this.audioPath});

  @override
  _AudioScrubberState createState() => _AudioScrubberState();
}

class _AudioScrubberState extends State<AudioScrubber> {
  late FlutterSoundPlayer _audioPlayer;
  double _progress = 0.0;
  double _duration = 0.0;
  bool _isPlaying = false;

  @override
  void initState() {
    super.initState();
    _audioPlayer = FlutterSoundPlayer();
    _audioPlayer.openAudioSession().then((value) {
      _audioPlayer.setSubscriptionDuration(Duration(milliseconds: 100));
    });
  }

  @override
  void dispose() {
    super.dispose();
    _audioPlayer.closeAudioSession();
    _audioPlayer = null;
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Slider(
          value: _progress,
          min: 0.0,
          max: _duration,
          onChanged: (value) {
            setState(() {
              _progress = value;
            });
          },
          onChangeEnd: (value) {
            _audioPlayer.seekToPlayer(Duration(milliseconds: value.toInt()));
          },
        ),
        Row(
          mainAxisAlignment: MainAxisAlignment.spaceEvenly,
          children: [
            IconButton(
              icon: Icon(_isPlaying ? Icons.pause : Icons.play_arrow),
              onPressed: () {
                if (_isPlaying) {
                  _audioPlayer.pausePlayer();
                } else {
                  _audioPlayer.playFilePath(widget.audioPath);
                }
                setState(() {
                  _isPlaying = !_isPlaying;
                });
              },
            ),
            IconButton(
              icon: Icon(Icons.stop),
              onPressed: () {
                _audioPlayer.stopPlayer();
                setState(() {
                  _isPlaying = false;
                  _progress = 0.0;
                });
              },
            ),
          ],
        ),
      ],
    );
  }
}
```

In the above code snippet, we define the `AudioScrubber` widget as a `StatefulWidget`, as it needs to maintain the state of the audio playback and progress bar.

The `initState` function initializes the `FlutterSoundPlayer` and sets the audio session duration. The `dispose` function cleans up resources when the widget is disposed.

The `Slider` widget is used to display the progress of the audio playback. The `value` property is bound to the `_progress` state variable. The `onChanged` callback updates the `_progress` variable when the user drags the progress bar. The `onChangeEnd` callback seeks the audio player to the specified position when the user releases the progress bar.

The `IconButton` widgets are used for controlling the audio playback. The play/pause functionality is toggled based on the `_isPlaying` state variable.

## Using the Audio Scrubbing Widget

To use the `AudioScrubber` widget, pass the audio file path as a parameter:

```dart
AudioScrubber(audioPath: 'path/to/audio/file.mp3'),
```

Replace `'path/to/audio/file.mp3'` with the actual path to your audio file.

## Conclusion

In this blog post, we have learned how to implement audio scrubbing functionality using the Flutter Sound package. With the `AudioScrubber` widget, users can easily navigate through an audio file by dragging a progress bar or using playback control buttons. This feature enhances the user experience of audio playback in your Flutter applications.

We encourage you to explore the Flutter Sound package further and customize the audio scrubbing widget to fit your specific needs.

#flutter #flutter_sound #audio_scrubbing
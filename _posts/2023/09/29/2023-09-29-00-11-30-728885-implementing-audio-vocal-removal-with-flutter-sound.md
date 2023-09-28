---
layout: post
title: "Implementing audio vocal removal with Flutter Sound"
description: " "
date: 2023-09-29
tags: [flutter, flutterSound]
comments: true
share: true
---

Flutter Sound is a powerful audio plugin for the Flutter framework that allows developers to work with audio files, record audio, and perform various audio processing tasks. In this tutorial, we'll explore how to implement audio vocal removal using Flutter Sound.

## Introduction to Vocal Removal

Vocal removal is a technique used to extract the instrumental part of an audio recording while suppressing or removing the vocal parts. This can be useful in scenarios where you need to create karaoke versions of songs or isolate specific instruments from a mix.

## Setting up Flutter Sound

Before we dive into vocal removal, let's set up Flutter Sound in our Flutter project. First, make sure you have Flutter and Dart installed on your machine. Then, create a new Flutter project or open an existing one.

Next, add the Flutter Sound dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_sound: ^X.X.X
```

Replace `X.X.X` with the latest version of Flutter Sound.

Run `flutter pub get` to fetch the dependencies.

## Implementing Vocal Removal

To implement vocal removal, we'll need to perform Audio Signal Processing (ASP) techniques to analyze and modify the audio waveform. Fortunately, Flutter Sound provides an AudioProcessing class that allows us to access and modify audio data in real-time.

Here's an example code snippet demonstrating how to implement vocal removal with Flutter Sound:

```dart
import 'package:flutter_sound/flutter_sound.dart';

// Initialize Flutter Sound
final flutterSound = FlutterSound();

// Open the input audio file
final audioPath = "path_to_your_audio_file.mp3";
await flutterSound.openAudioSession().then((value) => print('Audio session initialized'));
await flutterSound.startPlayer(audioPath);

// Set up the output audio file
final outputPath = "path_to_output_audio_file.mp3";
final outputStream = File(outputPath).openWrite();

// Define the vocal removal audio processing callback
void vocalRemovalCallback(dynamic buffer) {
  // Perform vocal removal algorithm on the buffer
  // ...

  // Write the modified buffer to the output stream
  outputStream.write(buffer);
}

// Configure the audio processing
await flutterSound.setSubscriptionDuration(0.01); // Set the buffer duration
await flutterSound.setVolume(1.0); // Set the audio playback volume

// Start the audio processing
await flutterSound.startAudioProcessing(vocalRemovalCallback);

// Wait for the processing to complete
await Future.delayed(Duration(seconds: 10));

// Stop the audio processing and close the streams
await flutterSound.stopAudioProcessing();
await outputStream.close();
await flutterSound.stopPlayer();
await flutterSound.closeAudioSession();
```

In this example, we first initialize Flutter Sound and open the audio session. Then, we start the player with the input audio file and set up the output file stream.

Next, we define the `vocalRemovalCallback` function, which is called for each processing buffer. Inside this callback, you can implement your vocal removal algorithm to modify the audio buffer.

We then set the necessary audio processing configurations and start the audio processing with the vocal removal callback. After a designated time (in this case, 10 seconds), we stop the audio processing, close the streams, and close the audio session.

## Conclusion

Flutter Sound provides a convenient way to implement audio vocal removal in Flutter applications. In this tutorial, you learned how to set up Flutter Sound and apply vocal removal techniques using the AudioProcessing class. With this knowledge, you can now create applications that perform advanced audio processing tasks, such as vocal removal, within the Flutter framework.

#flutter #flutterSound
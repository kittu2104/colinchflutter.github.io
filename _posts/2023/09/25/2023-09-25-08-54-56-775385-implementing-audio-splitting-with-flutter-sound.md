---
layout: post
title: "Implementing audio splitting with Flutter Sound"
description: " "
date: 2023-09-25
tags: [flutter, fluttersound]
comments: true
share: true
---

In this tutorial, we will explore how to split audio files using the Flutter Sound package in a Flutter application. Audio splitting is a common requirement in multimedia applications, allowing users to extract specific sections of audio files for various purposes.

## Prerequisites

Before we begin, make sure you have the following installed:
- Flutter SDK
- Flutter Sound package (version 10.1.0 or above)

## Overview

The Flutter Sound package provides a comprehensive set of functionalities for audio recording, playback, and manipulation. To split an audio file, we will make use of the provided methods to read the original file, extract the desired section, and save it as a new file.

## Implementation Steps

### Step 1: Import required packages

Add the following import statement to your Dart file:

```dart
import 'package:flutter_sound/flutter_sound.dart';
```

### Step 2: Initialize Flutter Sound

Initialize the Flutter Sound instance by creating a new object and calling the `openAudioSession()` method. This step is necessary to set up the audio session and permissions required for audio manipulation.

```dart
FlutterSoundPlayer _audioPlayer = FlutterSoundPlayer();

void initializeFlutterSound() async {
  await _audioPlayer.openAudioSession();
}
```

### Step 3: Read the source audio file

To split an audio file, we first need to read the original audio file. Use the `FlutterSoundPlayer().startPlayer()` method to start playing the audio file. Here is an example:

```dart
void playAudioFile(String filePath) async {
  await _audioPlayer.startPlayer(fromURI: filePath);
}
```

### Step 4: Extract the desired section

Once the audio file is playing, we can extract the desired section from the audio. Use the `FlutterSoundPlayer().setCurrentProgress()` method to set the playhead position to the desired starting point. Then, use the `FlutterSoundPlayer().setSubscriptionDuration()` method to specify the duration of the section to be extracted. After setting these values, use the `FlutterSoundPlayer().startPlayer()` method to play the audio with the specified settings.

```dart
void extractAudioSection(int startMilliseconds, int durationMilliseconds) async {
  await _audioPlayer.setCurrentProgress(startMilliseconds / 1000);
  await _audioPlayer.setSubscriptionDuration(Duration(milliseconds: durationMilliseconds));
  await _audioPlayer.startPlayer();
}
```

### Step 5: Save the extracted section

To save the extracted audio section as a new file, use the `FlutterSoundRecorder().startRecorder()` method. This method will start recording the audio output from the audio player and save it as a new file. Specify the output file path and format parameters accordingly.

```dart
void saveExtractedAudioSection(String outputPath) async {
  await _audioPlayer.startRecorder(toFile: outputPath, codec: Codec.aacADTS);
}
```

### Step 6: Clean up and cleanup

After extracting the desired section and saving it as a new file, remember to clean up and release the resources used by Flutter Sound. Call the `FlutterSoundPlayer().stopPlayer()` and `FlutterSoundPlayer().closeAudioSession()` methods to stop playing the audio and close the audio session.

```dart
void disposeFlutterSound() async {
  await _audioPlayer.stopPlayer();
  await _audioPlayer.closeAudioSession();
}
```

## Conclusion

In this tutorial, we learned how to split audio files using the Flutter Sound package. By following these steps, you can implement audio splitting functionality in your Flutter applications. Feel free to explore other features provided by the Flutter Sound package to enhance your multimedia apps.

#flutter #fluttersound
---
layout: post
title: "Building a sound recognition app with audio classification in Flutter"
description: " "
date: 2023-09-18
tags: [soundrecognition]
comments: true
share: true
---

In this tutorial, we will explore how to build a sound recognition app using audio classification in Flutter. Sound recognition can be useful in various applications, such as identifying specific sounds like sirens, alarms, or animal noises.

To get started, we will use the Flutter audio package `audioplayers` for playing audio files, and `tflite_flutter` package for audio classification using TensorFlow Lite models.

## Setting Up the Project
1. Create a new Flutter project using the Flutter CLI or your preferred IDE.
2. Open the `pubspec.yaml` file, and add the dependencies for `audioplayers` and `tflite_flutter` packages. Make sure to include the latest versions.
```yaml
dependencies:
  audioplayers: ^0.19.1
  tflite_flutter: ^2.3.0
```
3. Run `flutter pub get` to fetch and install the packages.

## Loading the TensorFlow Lite Model
1. Place your trained TensorFlow Lite audio classification model (with appropriate labels) in the project directory.
2. Open the `main.dart` file, import the dependencies, and create an instance of the `AudioPlayer` class from the `audioplayers` package.
```dart
import 'package:audioplayers/audioplayers.dart';
import 'package:tflite_flutter/tflite_flutter.dart';

AudioPlayer _audioPlayer = AudioPlayer();
```
3. Now, we will need to load our TensorFlow Lite model. Create a function called `loadModel()`, and call it in the `initState()` method.
```dart
Future<void> loadModel() async {
  try {
    await Tflite.loadModel(
      model: 'assets/audio_model.tflite',
      labels: 'assets/audio_labels.txt',
    );
  } catch (e) {
    throw 'Failed to load the model: $e';
  }
}

@override
void initState() {
  super.initState();
  loadModel();
}
```

## Implementing Sound Recognition
1. Next, let's write a function called `classifySound()` that takes an audio file path as a parameter and performs sound classification using the loaded model.
```dart
Future<void> classifySound(String audioFilePath) async {
  try {
    List<dynamic> results = await Tflite.runModelOnAudio(
      audioPath: audioFilePath,
      numResults: 1,
    );
    
    String label = results[0]['label'];
    
    // Do something with the recognized label
    // e.g., display it in the UI or trigger a specific action based on the recognized sound
    
  } catch (e) {
    throw 'Failed to run sound recognition: $e';
  }
}
```

2. To trigger sound classification, let's create a button in our UI. Add the following code inside the `build()` method of the `MyApp` widget:
```dart
FlatButton(
  onPressed: () {
    classifySound('path_to_audio_file.wav');
  },
  child: Text('Classify Sound'),
),
```

## Conclusion
In this tutorial, we have learned how to build a sound recognition app with audio classification in Flutter. By leveraging the `audioplayers` and `tflite_flutter` packages, we have explored loading a TensorFlow Lite model and performing sound classification on audio files. This opens up possibilities for creating apps that can identify specific sounds in real-time, enabling a wide range of applications in areas like security, robotics, and more.

Stay tuned for more exciting Flutter tutorials!

#flutter #soundrecognition
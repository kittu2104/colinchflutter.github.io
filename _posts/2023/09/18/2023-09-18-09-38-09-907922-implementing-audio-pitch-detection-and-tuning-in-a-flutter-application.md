---
layout: post
title: "Implementing audio pitch detection and tuning in a Flutter application"
description: " "
date: 2023-09-18
tags: [AudioPitchDetection]
comments: true
share: true
---

Flutter is a popular framework for building cross-platform mobile applications. If you are building a music-related application, you might want to implement pitch detection and tuning functionality. In this blog post, we will walk you through the process of implementing audio pitch detection and tuning in a Flutter application.

## Getting Started

To get started, you need to add the `audiofileplayer` and `pitch` packages to your `pubspec.yaml` file:

```yaml
dependencies:
  audiofileplayer: ^0.2.3
  pitch: ^0.1.2
```

After adding the dependencies, run `flutter pub get` to fetch the packages.

## Pitch Detection

To detect the pitch of an audio sample, we can use the `pitch` package. First, import the necessary packages:

```dart
import 'package:pitchdetector/pitchdetector.dart';
import 'package:audiofileplayer/audiofileplayer.dart';
```

Create an instance of the `Audio ` class to load and play the audio file:

```dart
Audio audio = Audio.load('./assets/sample_audio.wav');
audio.play();
```

Next, create an instance of the `PitchDetector` class and provide the audio as input:

```dart
PitchDetector pitchDetector = PitchDetector(audio);
```

To get the pitch of the audio, call the `getPitch` method:

```dart
double pitch = pitchDetector.getPitch();
```

You can use the obtained pitch value to display the detected note to the user or perform further operations.

## Tuning

Once you have the pitch value, you can implement tuning functionality in your Flutter application. In this example, we will demonstrate how to display the detected pitch value and allow the user to adjust it.

Create a slider widget to adjust the pitch:

```dart
double pitchValue = 0.0;

Slider(
  value: pitchValue,
  min: -100.0,
  max: 100.0,
  onChanged: (value) {
    setState(() {
      pitchValue = value;
    });
  },
),
```

Inside the `onChanged` callback, update the pitch value and trigger a rebuild of the widget tree.

To apply the tuning to the audio, you can use the `pitch` package's `changePitch` method:

```dart
Audio modifiedAudio = pitchDetector.changePitch(pitchValue);
```

The `changePitch` method returns a new `Audio` instance with the modified pitch. You can then play the modified audio for the user to hear the effect of the tuning.

## Conclusion

In this blog post, we have shown you how to implement audio pitch detection and tuning in a Flutter application. By using the `audiofileplayer` and `pitch` packages, you can easily detect the pitch of an audio sample and implement tuning functionality. This opens up possibilities for creating music-related applications that require pitch analysis and manipulation. Get creative with your Flutter app and bring out the musician in you!

#Flutter #AudioPitchDetection #Tuning
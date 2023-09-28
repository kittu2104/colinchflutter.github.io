---
layout: post
title: "Implementing audio reverb and echo effects with Flutter Sound"
description: " "
date: 2023-09-29
tags: [flutter, audioeffects]
comments: true
share: true
---

Flutter Sound is a powerful audio manipulation package that allows you to record, play, and manipulate audio files in your Flutter applications. In this blog post, we will explore how to implement audio reverb and echo effects using Flutter Sound.

## Getting Started

To get started, make sure you have Flutter Sound added as a dependency in your `pubspec.yaml` file:

```dart
dependencies:
  flutter_sound:
```

Then, run `flutter pub get` to fetch the package.

## Adding Reverb Effect

To add the reverb effect to an audio file, first, import the necessary packages:

```dart
import 'package:flutter_sound/flutter_sound.dart';
import 'package:flutter_sound_platform_interface/flutter_sound_recorder.dart';
```

Then, define a Flutter Sound instance and load the audio file:

```dart
FlutterSound flutterSound = FlutterSound();

// Load audio file
String path = 'path/to/audio/file';
await flutterSound.startPlayer(path);
```

Next, set up the reverb effect parameters:

```dart
double reverbMix = 0.7; // Reverb mix, range from 0.0 to 1.0
double reverbRoomSize = 0.5; // Reverb room size, range from 0.0 to 1.0
double reverbDamping = 0.3; // Reverb damping, range from 0.0 to 1.0
```

Apply the reverb effect to the audio file:

```dart
flutterSound.setPlayerEffects([EffectReverb(reverbMix, reverbRoomSize, reverbDamping)]);
```

Finally, play the modified audio file with the reverb effect:

```dart
await flutterSound.startPlayer(null); // Pass null to play the loaded file with effects
```

## Adding Echo Effect

Similar to adding the reverb effect, we'll first import the necessary packages:

```dart
import 'package:flutter_sound/flutter_sound.dart';
import 'package:flutter_sound_platform_interface/flutter_sound_recorder.dart';
```

Load the audio file and define the echo effect parameters:

```dart
FlutterSound flutterSound = FlutterSound();

// Load audio file
String path = 'path/to/audio/file';
await flutterSound.startPlayer(path);

double echoDelay = 0.3; // Echo delay in seconds
double echoDecay = 0.6; // Echo decay, range from 0.0 to 1.0
double echoMix = 0.5; // Echo mix, range from 0.0 to 1.0
```

Apply the echo effect to the audio file:

```dart
flutterSound.setPlayerEffects([EffectEcho(echoDelay, echoDecay, echoMix)]);
```

Finally, play the modified audio file with the echo effect:

```dart
await flutterSound.startPlayer(null); // Pass null to play the loaded file with effects
```

## Conclusion

In this tutorial, we explored how to implement audio reverb and echo effects using Flutter Sound. By applying these effects, you can add depth and richness to your audio playback in Flutter applications. Experiment with different parameters to achieve the desired audio effects and enhance the overall user experience.

Make sure to check out the Flutter Sound documentation for more details on available effects and customization options.

#flutter #audioeffects
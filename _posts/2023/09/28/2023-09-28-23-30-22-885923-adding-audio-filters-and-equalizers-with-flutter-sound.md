---
layout: post
title: "Adding audio filters and equalizers with Flutter Sound"
description: " "
date: 2023-09-28
tags: [flutter, audio, filters, equalizers]
comments: true
share: true
---

Audio filtering and equalizing are essential features in any audio processing application. With the Flutter Sound package, you can easily implement them into your Flutter application. In this blog post, we will guide you through the process of adding audio filters and equalizers with Flutter Sound.

## Getting Started

To get started, make sure you have Flutter and Flutter Sound installed on your development machine. If you haven't installed Flutter Sound yet, open the `pubspec.yaml` file of your Flutter project and add the following dependency:

```yaml
dependencies:
  flutter_sound: ^X.X.X
```

Replace `X.X.X` with the latest version of Flutter Sound.

Next, run `flutter packages get` to fetch the dependency.

## Applying Audio Filters

Flutter Sound provides various audio filters that you can apply to your audio streams. Let's start by applying a low-pass filter to an audio stream. First, initialize the Flutter Sound object:

```dart
import 'package:flutter_sound/flutter_sound.dart';

final FlutterSound flutterSound = FlutterSound();
```

Next, load an audio file or start recording audio:

```dart
// Loading audio file
await flutterSound.startPlayer(filePath);

// Recording audio
await flutterSound.startRecorder();
```

Once you have the audio stream running, you can apply the low-pass filter using the `FlutterSound.setFilter` method:

```dart
await flutterSound.setFilter(Effects.LowPassFilter, cutoffFrequency);
```

Replace `cutoffFrequency` with the desired cutoff frequency in Hz.

To remove the filter, call the `FlutterSound.setFilter` method with `Effects.None` as the filter type:

```dart
await flutterSound.setFilter(Effects.None);
```

## Implementing Equalizers

Equalizers allow you to modify the frequency response of the audio stream. Flutter Sound provides a set of predefined equalizer presets that you can use or customize.

To apply an equalizer preset, initialize the Flutter Sound object and load the audio stream as shown earlier. Then, call the `FlutterSound.setEqualizerBandLevel` method for each band:

```dart
await flutterSound.setEqualizerBandLevel(FlutterSound.defaultEQPreset, bandIndex, bandLevel);
```

Replace `FlutterSound.defaultEQPreset` with the desired equalizer preset and `bandIndex` with the index of the equalizer band (0-9). Adjust `bandLevel` to set the desired gain for the band in dB.

To disable the equalizer, reset the band levels to zero:

```dart
for (int bandIndex = 0; bandIndex <= FlutterSound.maxEQIndex; bandIndex++) {
  await flutterSound.setEqualizerBandLevel(FlutterSound.defaultEQPreset, bandIndex, 0);
}
```

## Conclusion

In this blog post, we explored how to add audio filters and equalizers to your Flutter application using the Flutter Sound package. By leveraging the capabilities of Flutter Sound, you can enhance the audio processing capabilities of your app and provide a seamless user experience. Experiment with different filters and equalizers to find the perfect sound for your application.

If you want to learn more about Flutter Sound and its features, refer to the official Flutter Sound documentation. Happy coding!

#flutter #audio #filters #equalizers
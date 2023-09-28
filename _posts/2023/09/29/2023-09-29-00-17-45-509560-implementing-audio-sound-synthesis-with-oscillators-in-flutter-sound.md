---
layout: post
title: "Implementing audio sound synthesis with oscillators in Flutter Sound"
description: " "
date: 2023-09-29
tags: [flutter, sound, synthesis, oscillator]
comments: true
share: true
---

Hey there, Flutter enthusiasts! In this blog post, we will explore how to implement audio sound synthesis with oscillators using the **Flutter Sound** package. With Flutter Sound, you can easily generate different types of audio effects and customize the sounds according to your requirements.

## What is audio sound synthesis?

Audio sound synthesis is the process of generating sound signals electronically. It involves creating various sounds by combining different frequencies, waveforms, and amplitudes. In the case of oscillators, we can generate simple waveforms like sine, square, triangle, or sawtooth.

## Getting started with Flutter Sound

Before we dive into the implementation, make sure you have the Flutter Sound package added to your Flutter project. Open your `pubspec.yaml` file and add the following dependency:

```dart
dependencies:
  flutter_sound: ^x.x.x
```

Replace `x.x.x` with the latest version of the Flutter Sound package.

Once you have added the dependency, run `flutter pub get` to fetch and install the package.

## Creating an oscillator

To create an oscillator waveform, Flutter Sound provides the `Oscillator` class. This class allows you to define various properties of the oscillator. Let's start by creating a simple sine wave oscillator:

```dart
import 'package:flutter_sound/flutter_sound.dart';

void main() {
  // Create an instance of the Oscillator class
  Oscillator oscillator = Oscillator();

  // Set the type of waveform (sine in this case)
  oscillator.setType(OscillatorType.sine);

  // Set the frequency of the oscillator
  oscillator.setFrequency(440);

  // Generate audio by rendering the oscillator waveform
  List<int> audioData = oscillator.render(numSamples: 44100);

  // Use the audioData for further processing or playback
}
```

In the above code, we created an instance of the `Oscillator` class and set the type to a sine waveform. We also set the frequency to 440 Hz, which corresponds to the A4 musical note. The `render` method generates the audio data based on the oscillator parameters.

## Playing the audio

To play the generated audio, we can utilize the features provided by Flutter Sound. Here's an example of how to play the audio using the `AudioPlayer` class:

```dart
import 'package:flutter_sound/flutter_sound.dart';

void playAudio(List<int> audioData) async {
  // Create an instance of the AudioPlayer class
  AudioPlayer audioPlayer = AudioPlayer();

  // Start playing the audio
  await audioPlayer.startPlayer(
    fromDataBuffer: audioData,
    codec: Codec.pcm16,
    numChannels: 1,
    sampleRate: 44100,
  );
}
```

In the above code, we created an instance of the `AudioPlayer` class and used the `startPlayer` method to start playing the audio. We provided the audio data, codec, number of channels, and the sample rate corresponding to the audio data we generated using the oscillator.

## Conclusion

And that's it! You have successfully implemented audio sound synthesis with oscillators in Flutter Sound. You can now create various waveforms and play them back using the Flutter Sound package. Experiment with different types of waveforms and parameters to achieve unique sounds and effects in your Flutter applications.

Don't forget to check out the official documentation of [**Flutter Sound**](https://pub.dev/packages/flutter_sound) for more advanced features and options.

#flutter #sound #synthesis #oscillator
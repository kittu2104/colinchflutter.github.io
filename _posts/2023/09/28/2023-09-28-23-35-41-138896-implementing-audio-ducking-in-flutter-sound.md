---
layout: post
title: "Implementing audio ducking in Flutter Sound"
description: " "
date: 2023-09-28
tags: [flutter, audio, ducking]
comments: true
share: true
---

When developing audio apps in Flutter, one useful feature to consider is audio ducking. Audio ducking is the ability to lower the volume of one audio source when another source starts playing, such as when a phone call comes in, allowing the user to focus on the call without being disturbed by loud background audio.

In this blog post, we will explore how to implement audio ducking in Flutter Sound, a popular audio plugin for Flutter apps.

## Getting Started with Flutter Sound

Before we dive into implementing audio ducking, let's start by setting up Flutter Sound in our Flutter project. Here are the steps to follow:

1. Install the Flutter Sound plugin by adding it to your `pubspec.yaml` file:

   ```yaml
   dependencies:
     flutter_sound: any
   ```

2. Run `flutter pub get` to fetch the plugin and its dependencies.

3. Import the Flutter Sound package in your Dart code:

   ```dart
   import 'package:flutter_sound/flutter_sound.dart';
   ```

4. Initialize Flutter Sound before using it:

   ```dart
   FlutterSound flutterSound = FlutterSound();
   flutterSound.openAudioSession();
   ```

## Implementing Audio Ducking

To implement audio ducking, we need to detect when another audio source, such as a phone call, starts playing. We can achieve this by using the `flutter_phone_state` package, which allows us to listen to phone state changes.

1. Follow the steps mentioned above to add `flutter_phone_state` to your project.

2. Import the `flutter_phone_state` package:

   ```dart
   import 'package:flutter_phone_state/flutter_phone_state.dart';
   ```

3. Add a `PhoneCallListener` to detect phone state changes:

   ```dart
   final phoneCallListener = PhoneCallListener(
     onCallStateChanged: (CallState callState) {
       if (callState == CallState.RINGING || callState == CallState.OFFHOOK) {
         // Pause or lower the volume of the audio using Flutter Sound API
         flutterSound.pausePlayer();
         // or
         flutterSound.setVolume(volume: 0.5);
       } else {
         // Resume or restore the audio volume
         flutterSound.resumePlayer();
         // or
         flutterSound.setVolume(volume: 1.0);
       }
     },
   );
   ```

4. Start listening for phone state changes:

   ```dart
   phoneCallListener.start();
   ```

By following the steps above, we can successfully implement audio ducking in Flutter Sound. Whenever a phone call is received or the user starts a call, the audio playback will be paused or the volume will be lowered to ensure the user can focus on the call. Once the call ends, the audio playback will resume or the volume will be restored to its original level.

## Conclusion

In this blog post, we explored how to implement audio ducking in Flutter Sound. By utilizing the `flutter_phone_state` package, we were able to detect phone state changes and adjust the audio playback accordingly using the Flutter Sound API. Audio ducking is an essential feature for audio apps to ensure a seamless user experience. Give it a try and enhance your Flutter audio app with audio ducking capabilities.

#flutter #audio #ducking
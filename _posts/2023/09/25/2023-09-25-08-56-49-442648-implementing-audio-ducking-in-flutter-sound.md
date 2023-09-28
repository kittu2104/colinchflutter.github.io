---
layout: post
title: "Implementing audio ducking in Flutter Sound"
description: " "
date: 2023-09-25
tags: [AudioDucking]
comments: true
share: true
---

Audio ducking is a technique used in audio applications to automatically reduce the volume of one audio source when another audio source is playing. This is commonly used in media players, video conferencing apps, and other applications where multiple audio streams are playing simultaneously.

In this article, we will explore how to implement audio ducking in a Flutter app using the `flutter_sound` package. Let's get started!

## Step 1: Add Dependencies

First, we need to add the `flutter_sound` package to our project's dependencies. Open the `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter_sound: ^X.Y.Z
```

Replace `X.Y.Z` with the latest version of the `flutter_sound` package.

After adding the dependency, run `flutter pub get` to download and install the package.

## Step 2: Initialize Flutter Sound

Next, we need to initialize the Flutter Sound plugin. Import the `flutter_sound` package at the top of your Dart file:

```dart
import 'package:flutter_sound/flutter_sound.dart';
```

Then, create an instance of `FlutterSoundPlayer` class:

```dart
FlutterSoundPlayer _flutterSoundPlayer = FlutterSoundPlayer();
```

## Step 3: Set Up Audio Ducking

To implement audio ducking, we need to define two audio categories: the primary category and the secondary category.

The primary category is the audio source that should dominate, while the secondary category is the audio source that should be ducked when the primary category is playing.

In Flutter Sound, we can achieve this using the `setCategory` method. For example, to set the primary category to `Playback`, and the secondary category to `Ambient`, use the following code:

```dart
_flutterSoundPlayer.setCategory('Playback', mixWithOthers: true);
_flutterSoundPlayer.setCategory('Ambient', mixWithOthers: false);
```

Here, `mixWithOthers: true` allows other audio sources to play simultaneously with the primary category, while `mixWithOthers: false` ensures that the secondary category is ducked when the primary category is playing.

## Step 4: Play Audio

To play audio, use the `startPlayer` method provided by the `FlutterSoundPlayer` class. Here's an example of playing a sound file:

```dart
_flutterSoundPlayer.startPlayer(filePath);
```

Replace `filePath` with the path to your audio file.

## Conclusion

In this tutorial, we learned how to implement audio ducking in a Flutter app using the `flutter_sound` package. By setting up appropriate audio categories and using the `startPlayer` method, we can achieve audio ducking effects in our app.

Remember to experiment and test with different audio categories to get the desired audio ducking behavior for your specific use case.

Now, you're ready to enhance your Flutter app by adding audio ducking functionality. Happy coding!

#Flutter #AudioDucking
---
layout: post
title: "Setting up Flutter Sound in a Flutter project"
description: " "
date: 2023-09-28
tags: [Fluttersound]
comments: true
share: true
---

Flutter Sound is a cross-platform audio library that provides an interface for recording, playing, and manipulating audio in a Flutter project. In this blog post, we will guide you through the process of setting up Flutter Sound in your Flutter project.

## Step 1: Create a new Flutter project

First, make sure you have Flutter installed on your system. If not, you can follow the official documentation to install it.

To create a new Flutter project, open a terminal or command prompt and run the following command:

```bash
flutter create flutter_sound_demo
cd flutter_sound_demo
```

## Step 2: Add Flutter Sound dependency to pubspec.yaml

Open the `pubspec.yaml` file in the root directory of your Flutter project and add the following lines under the `dependencies` section:

```yaml
dependencies:
  flutter_sound: ^x.x.x
```
*Please replace `x.x.x` with the latest version of Flutter Sound.*

Save the file and run the following command in the terminal to fetch the dependencies:

```bash
flutter pub get
```

## Step 3: Import and initialize Flutter Sound

In the Dart file where you want to use Flutter Sound, import the library at the top of the file:

```dart
import 'package:flutter_sound/flutter_sound.dart';
```

To initialize Flutter Sound, create an instance of the `FlutterSoundPlayer` class:

```dart
FlutterSoundPlayer _soundPlayer = FlutterSoundPlayer();
```

## Step 4: Use Flutter Sound capabilities

Once you have initialized Flutter Sound, you can start using its capabilities. Here are a few examples to get you started:

### Recording audio

To record audio, use the `startRecorder` method:

```dart
String path = 'path/to/save/audio.wav';
await _soundPlayer.startRecorder(toFile: path, codec: Codec.pcm16);
```

### Playing audio

To play audio from a file, use the `startPlayer` method:

```dart
String path = 'path/to/audio.wav';
await _soundPlayer.startPlayer(fromURI: path);
```

### Manipulating audio

Flutter Sound provides various methods for manipulating audio, such as controlling the volume, seeking to a specific position, and setting the playback rate. Here's an example of setting the playback rate:

```dart
_soundPlayer.setRate(2.0); // Sets the playback rate to 2x
```

## Conclusion

By following the steps outlined in this blog post, you have successfully set up Flutter Sound in your Flutter project. You can now start recording, playing, and manipulating audio in your app with ease. Happy coding!

#flutter #Fluttersound
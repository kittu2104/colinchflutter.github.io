---
layout: post
title: "Creating a white noise app with audio playback in Flutter"
description: " "
date: 2023-09-18
tags: [flutter, whitenoiseapp]
comments: true
share: true
---

White noise is a type of noise that contains all frequencies in equal measure. It is often used to enhance focus, promote relaxation, or help with sleep. In this tutorial, we will be creating a white noise app with audio playback functionality using Flutter, a popular cross-platform mobile app development framework.

## Prerequisites

Before we start, make sure you have Flutter installed on your machine. You can follow the official Flutter installation guide for your operating system.

## Setting up the project

1. Open your preferred IDE and create a new Flutter project.

2. Delete the contents of the `lib/main.dart` file and replace it with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:audioplayers/audioplayers.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final audioPlayer = AudioCache();

  void playWhiteNoise() {
    audioPlayer.play('white_noise.mp3');
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'White Noise App',
      home: Scaffold(
        appBar: AppBar(
          title: Text('White Noise App'),
        ),
        body: Center(
          child: RaisedButton(
            onPressed: playWhiteNoise,
            child: Text('Play White Noise'),
          ),
        ),
      ),
    );
  }
}
```

3. Create a new folder called `assets` in the root directory of your project.

4. Place a white noise audio file (in MP3 format) named `white_noise.mp3` inside the `assets` folder.

## Configuring the project

1. Open the `pubspec.yaml` file and add the following lines under the `assets` section:

```yaml
assets:
  - assets/white_noise.mp3
```

2. Run the following command in the terminal to fetch the dependencies:

```bash
flutter pub get
```

## Testing the app

1. Connect a physical device or start an emulator.

2. Run the app using the following command:

```bash
flutter run
```

3. The app should launch on your device or emulator. Press the "Play White Noise" button, and you should hear the white noise playing in the background.

## Conclusion

In this tutorial, we learned how to create a white noise app with audio playback functionality using Flutter. We utilized the `audioplayers` plugin for audio playback, and the `AudioCache` class to load and play the white noise audio file. With this foundation, you can further enhance the app by adding features such as volume control, different types of white noise, and timer functionality to automatically stop playback after a specified duration.

Give your mind a break and enjoy the relaxing benefits of white noise with your very own Flutter app!

#flutter #whitenoiseapp
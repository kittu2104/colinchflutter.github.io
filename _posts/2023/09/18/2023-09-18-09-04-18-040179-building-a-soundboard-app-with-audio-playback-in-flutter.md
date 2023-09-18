---
layout: post
title: "Building a soundboard app with audio playback in Flutter"
description: " "
date: 2023-09-18
tags: [Flutter, SoundboardApp]
comments: true
share: true
---

In this tutorial, we will be building a soundboard app using Flutter, a cross-platform framework for developing mobile applications. Our app will allow users to play different sound clips by tapping on buttons displayed on the screen. Let's get started!

## Prerequisites
Before we begin, make sure you have Flutter and Dart installed on your machine. You can follow the official Flutter installation guide to set up the necessary tools.

## Setting up the Project
1. Create a new Flutter project using the command `flutter create soundboard_app`.
2. Open the project in your preferred code editor.

## Designing the User Interface
1. Inside the `lib` directory, create a new file called `soundboard_screen.dart`.
2. Replace the default code with the following:

```dart
import 'package:flutter/material.dart';

class SoundboardScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Soundboard App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            SoundButton(
              soundName: 'Sound 1',
              soundPath: 'assets/sound1.mp3',
            ),
            SoundButton(
              soundName: 'Sound 2',
              soundPath: 'assets/sound2.mp3',
            ),
            // Add more SoundButton widgets for other sound clips
          ],
        ),
      ),
    );
  }
}

class SoundButton extends StatelessWidget {
  final String soundName;
  final String soundPath;

  SoundButton({required this.soundName, required this.soundPath});

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: () {
        // Logic to play the sound
      },
      child: Text(soundName),
    );
  }
}
```

## Adding Sound Clips
1. Create a new folder called `assets` at the root of your project.
2. Add the sound clips you want to use in your app to the `assets` folder. Make sure they have `.mp3` file extension.
3. Open the `pubspec.yaml` file and add the following code to include the assets:

```yaml
flutter:
  assets:
    - assets/
```

4. Save the changes and run `flutter pub get` in the terminal to fetch the assets.

## Playing Audio
1. Open the `soundboard_screen.dart` file.
2. Add the following imports at the top:

```dart
import 'package:audioplayers/audioplayers.dart';
import 'package:flutter/services.dart';
```

3. Inside the `SoundButton` widget, create an instance of `AudioPlayer`:

```dart
final AudioPlayer audioPlayer = AudioPlayer();
```

4. Modify the `onPressed` function of the `SoundButton` widget to play the sound clip:

```dart
onPressed: () {
  _playSound();
},
```

5. Add the `_playSound` function to the `SoundButton` widget:

```dart
void _playSound() async {
  await audioPlayer.stop();
  await audioPlayer.play(soundPath);
}
```

6. Save the changes and run the app using `flutter run`.

Congratulations! You have successfully built a soundboard app with audio playback using Flutter. Users can now tap on the sound buttons to play different sound clips. Feel free to customize the app further by adding more sound buttons or enhancing the UI. Happy coding!

## #Flutter #SoundboardApp
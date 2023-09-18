---
layout: post
title: "Building a nature sounds app with audio playback in Flutter"
description: " "
date: 2023-09-18
tags: [flutter, flutterdevelopment]
comments: true
share: true
---

Are you looking to build a soothing nature sounds app using Flutter? In this tutorial, we will guide you through the process of creating an app that plays relaxing nature sounds. We will leverage the builtin audio playback functionality provided by Flutter to achieve this.

## Prerequisites

Before we get started, make sure you have the following:

- Flutter SDK installed on your machine
- A text editor or an IDE of your choice

## Getting Started

Let's start by creating a new Flutter project. Open your terminal or command prompt and run the following command:

```dart
flutter create nature_sounds_app
```

This command will create a new Flutter project named "nature_sounds_app" in your current directory.

Next, navigate to the project directory:

```dart
cd nature_sounds_app
```

## Adding Dependencies

Our nature sounds app will rely on the audioplayers package to handle audio playback. Open the `pubspec.yaml` file in your project and add the following line to the dependencies section:

```yaml
dependencies:
  audioplayers: ^0.18.3
```

Save the file, and run the following command to install the dependencies:

```dart
flutter pub get
```

## Setting up the User Interface

Now, let's create the user interface for our app. Open the `lib/main.dart` file in your project and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() => runApp(NatureSoundsApp());

class NatureSoundsApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Nature Sounds App',
      theme: ThemeData(
        primarySwatch: Colors.green,
      ),
      home: SoundsPage(),
    );
  }
}

class SoundsPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Nature Sounds'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            // Place your UI components here
          ],
        ),
      ),
    );
  }
}
```

This code sets up a basic Flutter app with a `SoundsPage` as the home screen. Replace the placeholder comment inside the `Column` widget with your desired UI components such as buttons or a list of nature sounds.

## Handling Audio Playback

To play audio files in our app, we will leverage the `audioplayers` package. Open the `lib/main.dart` file and add the following import statement at the top:

```dart
import 'package:audioplayers/audioplayers.dart';
```

Under the `SoundsPage` class, create an instance of `AudioPlayer`:

```dart
final audioPlayer = AudioPlayer();
```

Next, add a method to play the audio file when a button is pressed:

```dart
void playAudio(String audioUrl) async {
  int result = await audioPlayer.play(audioUrl);
  if (result == 1) {
    // success
  }
}
```

You can call the `playAudio` method when a button is pressed in your UI. Ensure you pass the URL or file path of the audio file you want to play.

## Conclusion

Congratulations! You have successfully learned how to build a nature sounds app with audio playback support using Flutter. You can further enhance the app by adding more features like a timer or a playlist. Feel free to explore the `audioplayers` package documentation for more advanced functionality.

#flutter #flutterdevelopment
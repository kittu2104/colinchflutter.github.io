---
layout: post
title: "Building a MIDI controller app with audio playback in Flutter"
description: " "
date: 2023-09-18
tags: [flutter, MIDI]
comments: true
share: true
---

Flutter is a powerful cross-platform framework that allows developers to build beautiful and performant user interfaces. In this tutorial, we will learn how to build a MIDI controller app with audio playback using Flutter and take advantage of its rich ecosystem of packages.

## What is MIDI?

MIDI stands for Musical Instrument Digital Interface. It is a protocol that allows electronic musical instruments, computers, and other devices to communicate with each other. MIDI messages typically include information about notes, timing, velocity, and control changes.

## Requirements

To follow along with this tutorial, make sure you have the following:

- Flutter SDK: You can download it from the official Flutter website.
- A code editor of your choice, such as Visual Studio Code or Android Studio.
- Basic understanding of Flutter and Dart programming language.

## Project Setup

First, let's create a new Flutter project. Open your terminal or command prompt and run the following command:

```dart
flutter create midi_controller_app
```

Next, navigate to the project directory:

```dart
cd midi_controller_app
```

## MIDI Playback

To handle MIDI playback, we will use the `midi` package. Add it as a dependency in your `pubspec.yaml` file:

```dart
dependencies:
  flutter:
   sdk: flutter

  midi: ^0.1.1
```

After saving the changes, run the following command in your terminal to download the dependencies:

```dart
flutter pub get
```

## Building the UI

Now, let's create a basic user interface for our MIDI controller app. Open the `lib/main.dart` file and replace its contents with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MidiControllerApp());
}

class MidiControllerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'MIDI Controller',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('MIDI Controller'),
        ),
        body: Center(
          child: Text('Hello MIDI!'),
        ),
      ),
    );
  }
}
```

This sets up a basic Flutter app with a centered text widget that displays "Hello MIDI!".

## Handling MIDI Input

To handle MIDI input, we will use the `flutter_midi` package. Add it as a dependency in your `pubspec.yaml` file:

```dart
dependencies:
  flutter:
   sdk: flutter

  midi: ^0.1.1
  flutter_midi: ^0.1.1
```

Run the `flutter pub get` command to download the dependencies.

Next, open the `lib/main.dart` file and add the following imports:

```dart
import 'package:flutter_midi/flutter_midi.dart';
import 'package:midi/midi.dart';
```

Inside the `MidiControllerApp` class, add a `MidiController` widget as the body of the `Scaffold`. The `MidiController` widget will be responsible for handling MIDI input and playback. Here's the modified code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_midi/flutter_midi.dart';
import 'package:midi/midi.dart';

void main() {
  runApp(MidiControllerApp());
}

class MidiControllerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'MIDI Controller',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('MIDI Controller'),
        ),
        body: MidiController(),
      ),
    );
  }
}

class MidiController extends StatefulWidget {
  @override
  _MidiControllerState createState() => _MidiControllerState();
}

class _MidiControllerState extends State<MidiController> {
  Midi midi = Midi();

  @override
  void initState() {
    super.initState();
    initMIDI();
  }

  void initMIDI() async {
    await midi.start();

    midi.addListener((MidiEvent event) {
      // Handle MIDI events
    });
  }

  @override
  void dispose() {
    midi.stop();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Text('MIDI Controller'),
    );
  }
}
```

In this code, we create a `Midi` object and initialize it in the `initMIDI` function. We also add a listener to handle MIDI events.

## Conclusion

In this tutorial, we learned how to build a MIDI controller app with audio playback in Flutter. We covered the basics of setting up the project, handling MIDI input, and building the UI. Flutter's rich ecosystem of packages, such as `midi` and `flutter_midi`, makes it easy to integrate MIDI functionality into your apps. Feel free to explore more features of these packages to enhance your MIDI controller app.

#flutter #MIDI #audio #FlutterTutorial
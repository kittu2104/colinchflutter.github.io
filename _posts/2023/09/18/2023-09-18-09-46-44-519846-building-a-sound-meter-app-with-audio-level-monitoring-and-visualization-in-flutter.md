---
layout: post
title: "Building a sound meter app with audio level monitoring and visualization in Flutter"
description: " "
date: 2023-09-18
tags: [soundmeter]
comments: true
share: true
---

Are you looking to build a sound meter app with audio level monitoring and visualization in Flutter? Look no further! In this tutorial, we will guide you through the process of creating a sound meter app using Flutter, a powerful cross-platform framework.

## Prerequisites
Before we dive into the details, make sure you have the following prerequisites in place:

1. Flutter SDK installed on your system.
2. A code editor (such as Visual Studio Code or Android Studio) for writing Flutter code.

## Getting Started
To get started, open your terminal and create a new Flutter project using the following command:

```bash
flutter create sound_meter_app
```

Navigate to the newly created project directory:

```bash
cd sound_meter_app
```

Now, let's open the project in your favorite code editor and make the necessary changes to the `lib/main.dart` file.

## Implementing the Sound Meter
To implement the sound meter functionality, we need to make use of the `audio` package provided by the Flutter community. Add the `audio` package to your `pubspec.yaml` file:

```yaml
dependencies:
  audio: ^0.7.4
```

Save the file and run the following command to fetch the package dependencies:

```bash
flutter pub get
```

## Code Implementation
Now, let's dive into the code implementation. Replace the existing code in `lib/main.dart` with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:audio/audio.dart';

void main() {
  runApp(SoundMeterApp());
}

class SoundMeterApp extends StatefulWidget {
  SoundMeterAppState createState() => SoundMeterAppState();
}

class SoundMeterAppState extends State<SoundMeterApp> {
  Audio audio;
  double currentDecibel = 0.0;

  @override
  void initState() {
    super.initState();
    audio = Audio();
    audio.start(onAudioData);
  }

  void onAudioData(List<int> data) {
    double maxDecibel = 0.0;
    for (var value in data) {
      double decibel = 20.0 * log10(value / 32767.0);
      if (decibel > maxDecibel) {
        maxDecibel = decibel;
      }
    }
    setState(() {
      currentDecibel = maxDecibel;
    });
  }

  @override
  void dispose() {
    audio.dispose();
    super.dispose();
  }

  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Sound Meter App'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Text(
                'Current Decibel Level:',
                style: TextStyle(
                  fontSize: 24.0,
                  fontWeight: FontWeight.bold,
                ),
              ),
              SizedBox(height: 20.0),
              Text(
                '$currentDecibel dB',
                style: TextStyle(
                  fontSize: 48.0,
                  fontWeight: FontWeight.bold,
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

## Understanding the Code
In the above code, we import the necessary packages and define our `SoundMeterApp` widget as a stateful widget. Inside the `SoundMeterAppState` class, we initialize the required instances and start the audio recording using the `audio` package.

The `onAudioData` method is called whenever new audio data is received. We calculate the decibel level for each data point and update the UI accordingly using `setState`.

In the `build` method, we define the app's UI, which includes an `AppBar` and a column with text widgets to display the current decibel level.

## Running the App
To run the app, connect your device or emulator and use the following command:

```bash
flutter run
```

You should now see the Sound Meter app running on your device/emulator, displaying the current decibel level.

## Conclusion
In this tutorial, you learned how to build a sound meter app with audio level monitoring and visualization using Flutter. With its powerful audio package and UI capabilities, Flutter makes it easy to create cross-platform sound meter apps.

#flutter #soundmeter
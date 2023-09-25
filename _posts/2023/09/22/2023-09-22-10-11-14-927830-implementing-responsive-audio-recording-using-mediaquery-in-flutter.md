---
layout: post
title: "Implementing responsive audio recording using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [audio]
comments: true
share: true
---

With the growing popularity of mobile applications, audio recording has become an essential feature in many apps. In this tutorial, we will explore how to implement responsive audio recording using `MediaQuery` in Flutter.

## Prerequisites

To follow along with this tutorial, make sure you have Flutter and Dart installed on your machine. You can install them by following the official Flutter documentation.

## Setting up the Project

Let's start by creating a new Flutter project. Open your terminal and run the following command:

```
flutter create responsive_audio_recording
```

Once the project is created, navigate to the directory using `cd responsive_audio_recording` and open it in your preferred code editor.

## Designing the UI

The first step is to design the user interface for our audio recording feature. For simplicity, we will create a simple layout with a record button and a timer.

Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(ResponsiveAudioRecordingApp());
}

class ResponsiveAudioRecordingApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Audio Recording',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: AudioRecordingScreen(),
    );
  }
}

class AudioRecordingScreen extends StatefulWidget {
  @override
  _AudioRecordingScreenState createState() => _AudioRecordingScreenState();
}

class _AudioRecordingScreenState extends State<AudioRecordingScreen> {
  bool isRecording = false;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Audio Recording'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Icon(
              Icons.mic,
              size: 80,
              color: isRecording ? Colors.red : Colors.grey,
            ),
            SizedBox(height: 16),
            Text(
              isRecording ? 'Recording...' : 'Tap to Record',
              style: TextStyle(fontSize: 24),
            ),
            SizedBox(height: 16),
            ElevatedButton(
              onPressed: () {
                setState(() {
                  isRecording = !isRecording;
                });
              },
              child: Text(isRecording ? 'Stop Recording' : 'Start Recording'),
            ),
          ],
        ),
      ),
    );
  }
}
```

In the above code, we have defined a simple UI layout with an `AppBar`, an `Icon` to represent the microphone, a `Text` widget to display the recording status, and an `ElevatedButton` for starting and stopping the recording.

We have also used the `isRecording` boolean variable to toggle the recording state and update the UI accordingly.

## Making the UI Responsive

To make our audio recording feature responsive, we will make use of the `MediaQuery` class provided by Flutter. This class enables us to retrieve information about the current device's screen size, orientation, and other characteristics.

Open the `lib/main.dart` file and replace the `build` method of the `_AudioRecordingScreenState` class with the following code:

```dart
@override
Widget build(BuildContext context) {
  final mediaQuery = MediaQuery.of(context);

  return Scaffold(
    appBar: AppBar(
      title: Text('Responsive Audio Recording'),
    ),
    body: Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          Icon(
            Icons.mic,
            size: mediaQuery.size.width * 0.2,
            color: isRecording ? Colors.red : Colors.grey,
          ),
          SizedBox(height: 16),
          Text(
            isRecording ? 'Recording...' : 'Tap to Record',
            style: TextStyle(fontSize: mediaQuery.size.width * 0.04),
          ),
          SizedBox(height: 16),
          ElevatedButton(
            onPressed: () {
              setState(() {
                isRecording = !isRecording;
              });
            },
            child: Text(isRecording ? 'Stop Recording' : 'Start Recording'),
          ),
        ],
      ),
    ),
  );
}
```

In the above code, we have accessed the `MediaQuery` using `MediaQuery.of(context)`. We then used the `mediaQuery.size.width` property to dynamically adjust the size of the microphone `Icon` and the font size of the recording status `Text` based on the device's screen width.

## Conclusion

In this tutorial, we have learned how to implement responsive audio recording in Flutter using `MediaQuery`. By leveraging the properties provided by `MediaQuery`, we can make our app's user interface adapt to different device sizes and orientations, providing a better user experience.

Remember, responsive design plays a crucial role in creating a user-friendly app that can be used across various devices. Take advantage of `MediaQuery` to ensure your app's audio recording feature works seamlessly on different screen sizes.

#flutter #audio #recording #responsivedesign
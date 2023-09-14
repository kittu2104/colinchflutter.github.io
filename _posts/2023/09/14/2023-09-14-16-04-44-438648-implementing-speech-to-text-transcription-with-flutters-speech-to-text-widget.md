---
layout: post
title: "Implementing speech-to-text transcription with Flutter's speech-to-text widget"
description: " "
date: 2023-09-14
tags: [flutter, speechtotext]
comments: true
share: true
---

Recently, speech recognition and transcription have become an essential part of many applications. Whether it's implementing voice commands, live transcriptions, or voice input, integrating speech-to-text functionality can greatly enhance the user experience. 

In this blog post, we will explore how to implement speech-to-text transcription using Flutter's built-in speech-to-text widget. Flutter is a cross-platform framework that allows you to build beautiful and performant mobile applications for Android and iOS, making it an ideal choice for adding speech recognition capabilities to your app.

## Setting up the project
First, make sure you have Flutter and Dart installed on your machine. If you don't, head over to the Flutter website and follow the installation instructions.

Next, create a new Flutter project using the following command in your terminal:

```dart
flutter create speech_to_text_app
```

Once the project is created, navigate to the project directory:

```dart
cd speech_to_text_app
```

## Adding the speech-to-text plugin
Flutter provides a plugin called `speech_to_text` that allows us to integrate speech-to-text transcription into our application. To add the plugin to our project, open the `pubspec.yaml` file and add the following under the `dependencies` section:

```dart
dependencies:
  flutter:
    sdk: flutter
  speech_to_text: ^3.0.0
```

Save the file and run the following command to install the plugin:

```dart
flutter pub get
```

## Implementing speech-to-text functionality
Now that we have set up our project and added the necessary plugin, let's implement the speech-to-text functionality. Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:speech_to_text/speech_to_text.dart' as stt;

void main() {
  runApp(SpeechToTextApp());
}

class SpeechToTextApp extends StatefulWidget {
  @override
  _SpeechToTextAppState createState() => _SpeechToTextAppState();
}

class _SpeechToTextAppState extends State<SpeechToTextApp> {
  stt.SpeechToText _speech;
  bool _isListening = false;
  String _transcription = '';

  @override
  void initState() {
    super.initState();
    _speech = stt.SpeechToText();
  }

  void _listen() async {
    if (!_isListening) {
      bool available = await _speech.initialize();
      if (available) {
        setState(() {
          _isListening = true;
        });
        _speech.listen(
          onResult: (result) => setState(() {
            _transcription = result.recognizedWords;
          }),
        );
      }
    } else {
      setState(() {
        _isListening = false;
      });
      _speech.stop();
    }
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Speech to Text'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text(
                'Transcription:',
                style: TextStyle(fontWeight: FontWeight.bold),
              ),
              Text(
                _transcription,
                style: TextStyle(fontStyle: FontStyle.italic),
              ),
              SizedBox(height: 20),
              FloatingActionButton(
                onPressed: _listen,
                child: Icon(_isListening ? Icons.mic : Icons.mic_none),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

This code sets up a basic Flutter application that listens for speech input and updates the transcription in real-time. The `speech_to_text` plugin is used to handle the speech recognition functionality, and the UI is a simple column with a transcription display and a microphone button.

## Running the app
To run the application, connect your device or start the emulator and execute the following command:

```dart
flutter run
```

The app should launch on your device or emulator, and you can start speaking to see the transcription update in real-time.

## Conclusion
Integrating speech-to-text transcription into your Flutter application can provide significant benefits for user experience. In this blog post, we explored how to implement speech recognition using Flutter's `speech_to_text` plugin. With this knowledge, you can now enhance your Flutter applications with voice input, voice commands, or live transcriptions. Happy coding!

#flutter #speechtotext
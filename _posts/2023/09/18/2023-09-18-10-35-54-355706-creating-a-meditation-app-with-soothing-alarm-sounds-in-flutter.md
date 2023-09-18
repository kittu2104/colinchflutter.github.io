---
layout: post
title: "Creating a meditation app with soothing alarm sounds in Flutter"
description: " "
date: 2023-09-18
tags: [meditationapp]
comments: true
share: true
---

In this tutorial, we will learn how to create a meditation app using Flutter, a popular cross-platform framework for building mobile applications. Our meditation app will feature soothing alarm sounds to help users relax and focus during their meditation sessions.

## Requirements

Before we jump into the implementation, make sure you have the following setup:

- Flutter SDK installed on your machine
- A code editor (such as VS Code or Android Studio)
- Basic knowledge of Dart programming language and Flutter framework

## Getting Started

1. Start by creating a new Flutter project using the Flutter CLI:
   ```dart
   flutter create meditation_app
   ```

2. Open the project in your preferred code editor.

3. Remove the default code in the `lib/main.dart` file and replace it with the following code:

   ```dart
   import 'package:flutter/material.dart';

   void main() {
     runApp(MeditationApp());
   }

   class MeditationApp extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return MaterialApp(
         title: 'Meditation App',
         theme: ThemeData(
           primarySwatch: Colors.blue,
         ),
         home: HomePage(),
       );
     }
   }

   class HomePage extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(
           title: Text('Meditation App'),
         ),
         body: Center(
           child: Text(
             'Welcome to the Meditation App!',
             style: TextStyle(fontSize: 24),
           ),
         ),
       );
     }
   }
   ```

4. Save the changes and run the app using the command:
   ```dart
   flutter run
   ```

   You should see a basic app with the title "Meditation App" on the app bar and a centered text saying "Welcome to the Meditation App!".

## Adding Alarm Sounds

Now let's add soothing alarm sounds to our meditation app.

1. Download the audio files of the soothing alarm sounds you want to include in your app. Place them in the `assets` folder of your Flutter project.

2. Open the `pubspec.yaml` file of your project and add the following lines inside the `flutter` section:

   ```yaml
   assets:
     - assets/
   ```

   This will ensure that the assets folder is included when building the app.

3. Next, create a new Dart file called `sound_player.dart` and add the following code:

   ```dart
   import 'package:audioplayers/audio_cache.dart';

   class SoundPlayer {
     static Future<void> playSound(String soundPath) async {
       AudioCache audioCache = AudioCache();
       await audioCache.play(soundPath);
     }
   }
   ```

   This class uses the `audioplayers` package to play the alarm sounds.

4. Now, open the `HomePage` class in the `main.dart` file, and modify the `build` method to add buttons for playing the alarm sounds:

   ```dart
   import 'package:flutter/material.dart';
   import 'sound_player.dart';

   class HomePage extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(
           title: Text('Meditation App'),
         ),
         body: Center(
           child: Column(
             mainAxisAlignment: MainAxisAlignment.center,
             children: [
               Text(
                 'Welcome to the Meditation App!',
                 style: TextStyle(fontSize: 24),
               ),
               RaisedButton(
                 child: Text('Play Sound 1'),
                 onPressed: () {
                   SoundPlayer.playSound('assets/sound1.mp3');
                 },
               ),
               RaisedButton(
                 child: Text('Play Sound 2'),
                 onPressed: () {
                   SoundPlayer.playSound('assets/sound2.mp3');
                 },
               ),
             ],
           ),
         ),
       );
     }
   }
   ```

   This code adds two buttons, "Play Sound 1" and "Play Sound 2". When a button is pressed, the corresponding sound will be played.

5. Save your changes and run the app again. Now, when you click on the buttons, the respective alarm sounds should play.

## Conclusion

In this tutorial, we learned how to create a basic meditation app using Flutter and incorporate soothing alarm sounds. You can enhance this app further by adding more features like meditation timers, guided meditation sessions, and a calm UI design. With Flutter's flexibility and extensive widget library, the possibilities are endless.

#flutter #meditationapp
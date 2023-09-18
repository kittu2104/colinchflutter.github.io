---
layout: post
title: "Implementing different alarm sounds in Flutter using Alarm Manager"
description: " "
date: 2023-09-18
tags: [alarm]
comments: true
share: true
---

When building alarm clock apps or reminder apps in Flutter, it is important to provide users with different alarm sounds to choose from. Having a variety of alarm sounds can enhance the user experience and customize the app to suit individual preferences. In this article, we will explore how to implement different alarm sounds in Flutter using the Alarm Manager package.

## Setting up the Project

Before we can implement different alarm sounds, let's set up a basic Flutter project and install the required dependencies.

1. Create a new Flutter project by running the following command:

```shell
flutter create alarm_app
```

2. Open the project directory:

```shell
cd alarm_app
```

3. Open the `pubspec.yaml` file and add the Alarm Manager dependency:

```yaml
dependencies:
  alarm_manager: ^0.4.1
```

4. Save the `pubspec.yaml` file and run the following command to fetch the dependencies:

```shell
flutter pub get
```

## Implementing the Alarm Manager

Now that our project is set up, let's dive into implementing the alarm manager functionality with the ability to play different alarm sounds.

1. Import the required dependencies in the `main.dart` file:

```dart
import 'package:flutter/material.dart';
import 'package:alarm_manager/alarm_manager.dart';
```

2. Create a function to set up the alarm:

```dart
void setupAlarm() {
  AlarmManager.instance.addAlarm(
    Duration(seconds: 10), // Set the time for the alarm to trigger after 10 seconds
    alarmID: 1,
    soundUri: "path_to_sound_file.mp3", // Replace with the actual path to the sound file
  );
}
```

3. Use the `setupAlarm` function in the `build` method of the `MyApp` widget:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    setupAlarm(); // Call the setupAlarm function
    
    return MaterialApp(
      // Rest of your app code
    );
  }
}
```

4. Customize the `setupAlarm` function to allow users to select different alarm sounds:

```dart
void setupAlarm(String soundUri) {
  AlarmManager.instance.addAlarm(
    Duration(seconds: 10),
    alarmID: 1,
    soundUri: soundUri,
  );
}
```

5. Integrate a UI to allow users to select different alarm sounds. This can be done using Flutter's `ListView` widget and an `onTap` event handler:

```dart
class SoundSelectionPage extends StatelessWidget {
  final List<String> alarmSounds = [
    "sound1.mp3",
    "sound2.mp3",
    "sound3.mp3",
  ];

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: alarmSounds.length,
      itemBuilder: (context, index) {
        final soundUri = alarmSounds[index];
        return ListTile(
          title: Text(soundUri),
          onTap: () {
            setupAlarm(soundUri);
            Navigator.pop(context); // Navigate back to the previous screen
          },
        );
      },
    );
  }
}
```

## Conclusion

By implementing different alarm sounds in Flutter using the Alarm Manager package, we can provide users with a customizable experience and enhance the functionality of alarm clock or reminder apps. This gives users the ability to select alarm sounds that resonate with their preferences, making the overall experience more enjoyable.

Remember to import the necessary dependencies, set up the alarm using the `addAlarm` method, and integrate a UI for users to select different alarm sounds.

#flutter #alarm-app
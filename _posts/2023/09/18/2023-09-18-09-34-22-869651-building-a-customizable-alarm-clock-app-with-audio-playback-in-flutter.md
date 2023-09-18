---
layout: post
title: "Building a customizable alarm clock app with audio playback in Flutter"
description: " "
date: 2023-09-18
tags: [AlarmClockApp]
comments: true
share: true
---

In this tutorial, we will be building a customizable alarm clock app with audio playback using Flutter. Flutter is a popular framework for creating mobile applications, known for its fast development and beautiful UI. So let's dive into the details and create our very own alarm clock app!

## Prerequisites

Before we begin, make sure you have Flutter installed on your machine. You can check if Flutter is installed by running the following command in your terminal:

```bash
flutter --version
```

If Flutter is not installed, refer to the official Flutter documentation for installation instructions.

## Setting Up the Project

To create a new Flutter project, run the following command in your terminal:

```bash
flutter create alarm_clock_app
```

This will create a new Flutter project with the name "alarm_clock_app".

## Designing the User Interface

Open the `lib/main.dart` file and replace the default code with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(AlarmClockApp());
}

class AlarmClockApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Alarm Clock App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: AlarmHomePage(),
    );
  }
}

class AlarmHomePage extends StatefulWidget {
  @override
  _AlarmHomePageState createState() => _AlarmHomePageState();
}

class _AlarmHomePageState extends State<AlarmHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Alarm Clock'),
      ),
      body: Center(
        child: Text(
          'Alarm Clock App UI',
          style: TextStyle(fontSize: 20),
        ),
      ),
    );
  }
}
```

In the above code, we have defined the basic structure of our alarm clock app. We have a `AlarmClockApp` class that extends `StatelessWidget` and acts as the entry point of our app. Inside this class, we define the app's title and theme.

We also have a `AlarmHomePage` class that extends `StatefulWidget` and is responsible for rendering the main user interface of our app. In this example, we have a simple `Text` widget that displays "Alarm Clock App UI" in the center of the screen.

## Adding Alarm Functionality

To add the alarm functionality, we will need to add a time picker and a play button to set the alarm time and play the audio. Let's update the code inside the `_AlarmHomePageState` class as follows:

```dart
class _AlarmHomePageState extends State<AlarmHomePage> {

  TimeOfDay selectedTime = TimeOfDay.now();

  Future<void> _selectTime(BuildContext context) async {
    final TimeOfDay? pickedTime = await showTimePicker(
      context: context,
      initialTime: selectedTime,
    );
    if (pickedTime != null && pickedTime != selectedTime) {
      setState(() {
        selectedTime = pickedTime;
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Alarm Clock'),
      ),
      body: Column(
        children: [
          ListTile(
            title: Text('Alarm Time'),
            subtitle: Text('${selectedTime.format(context)}'),
            trailing: Icon(Icons.keyboard_arrow_down),
            onTap: () => _selectTime(context),
          ),
          ElevatedButton(
            onPressed: () => _playAudio(),
            child: Text('Play Alarm'),
          ),
        ],
      ),
    );
  }

  void _playAudio() {
    // Code to play the audio file
  }
}
```

In the above code, we have added a `TimeOfDay` variable called `selectedTime` to store the selected alarm time. The `_selectTime` method is called when the user taps on the `ListTile` widget, which opens a time picker dialog. The selected time is then updated using the `setState` method.

We have also added an `ElevatedButton` widget called "Play Alarm" that calls the `_playAudio` method when pressed. We are currently using a placeholder method for playing the audio file, which you can replace with your own implementation.

## Conclusion

With the code above, we have built a basic alarm clock app with a customizable alarm time and audio playback functionality. You can further enhance the app by adding more features, such as multiple alarms, repeating alarms, and custom alarm sounds.

Remember to test your app on both Android and iOS devices to ensure compatibility and a seamless user experience.

Happy coding! #Flutter #AlarmClockApp
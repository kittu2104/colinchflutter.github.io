---
layout: post
title: "Building a music player UI using ListView in Flutter."
description: " "
date: 2023-09-15
tags: [flutterdev]
comments: true
share: true
---

Flutter is a popular cross-platform framework that allows developers to build beautiful and functional user interfaces for both Android and iOS. In this tutorial, we will explore how to create a music player UI using the ListView widget in Flutter.

## Prerequisites

Before we begin, make sure you have Flutter installed on your machine. You can refer to the official Flutter documentation for installation instructions.

## Getting Started

To get started, create a new Flutter project using the following command in your terminal:

```shell
flutter create music_player
```

This will create a new Flutter project called "music_player". 

## Setting up the UI

Open the project in your preferred code editor and navigate to the `lib` directory. Open the `main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MusicPlayerApp());
}

class MusicPlayerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Music Player',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MusicPlayerScreen(),
    );
  }
}

class MusicPlayerScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Music Player'),
      ),
      body: ListView.builder(
        itemCount: 10, // Replace with actual music list size
        itemBuilder: (BuildContext context, int index) {
          return ListTile(
            title: Text('Song $index'),
            subtitle: Text('Artist $index'),
            leading: Icon(Icons.music_note),
            trailing: Icon(Icons.play_circle_outline),
          );
        },
      ),
    );
  }
}
```

In the code above, we have defined a simple Flutter app with a MusicPlayerApp class as our root widget. Inside the MusicPlayerScreen widget, we have used a ListView.builder to display a list of music items. Replace the `itemCount` property value with the actual size of your music list.

## Running the App

To run the app, connect a device or start the simulator, and run the following command in your terminal:

```shell
flutter run
```

This will launch the app on your device or simulator. You should now see a simple music player screen with a list of songs.

## Conclusion

In this tutorial, we have learned how to build a music player UI using the ListView widget in Flutter. The ListView.builder allows us to efficiently display a large list of items with minimal performance overhead. Flutter makes it easy to create beautiful and responsive UIs for mobile apps.

#flutter #flutterdev
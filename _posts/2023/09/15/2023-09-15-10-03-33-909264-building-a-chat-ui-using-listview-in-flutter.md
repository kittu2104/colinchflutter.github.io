---
layout: post
title: "Building a chat UI using ListView in Flutter."
description: " "
date: 2023-09-15
tags: []
comments: true
share: true
---

In this tutorial, we will learn how to create a chat user interface (UI) using the ListView widget in Flutter. The ListView widget provides a scrollable list of child widgets that we can use to display messages in a chat application.

## Prerequisites

Make sure you have Flutter and Dart set up on your local development environment.

## Step 1: Set up a new Flutter project

Create a new Flutter project using the following command:

```bash
flutter create chat_app
```

## Step 2: Update the pubspec.yaml file

Open the `pubspec.yaml` file in your project and add the `flutter_svg` package as a dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_svg: ^0.18.0
```

Then, run `flutter pub get` in your terminal to fetch the dependencies.

## Step 3: Create a new Flutter widget

Create a new file called `chat_screen.dart` in the `lib` folder. This file will contain our chat screen UI. Add the following code:

```dart
import 'package:flutter/material.dart';

class ChatScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Chat App"),
      ),
      body: ListView.builder(
        itemCount: 10,
        itemBuilder: (BuildContext context, int index) {
          return ListTile(
            title: Text("Message $index"),
          );
        },
      ),
    );
  }
}
```

## Step 4: Update the main.dart file

Open the `main.dart` file in the `lib` folder and replace the default `MyApp` widget with the following code:

```dart
import 'package:flutter/material.dart';
import 'chat_screen.dart';

void main() {
  runApp(ChatApp());
}

class ChatApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "Chat App",
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: ChatScreen(),
    );
  }
}
```

## Step 5: Run the application

Save your files and run the application using the following command:

```bash
flutter run
```

Now, you should see a chat screen with 10 default messages displayed in a scrollable list using the ListView widget.

## Conclusion

In this tutorial, we have learned how to create a chat user interface using the ListView widget in Flutter. You can customize the list items in the ListView.builder according to your requirements, such as showing user avatars or message timestamps.
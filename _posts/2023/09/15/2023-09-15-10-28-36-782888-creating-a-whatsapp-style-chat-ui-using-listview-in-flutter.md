---
layout: post
title: "Creating a WhatsApp-style chat UI using ListView in Flutter."
description: " "
date: 2023-09-15
tags: [chatUI]
comments: true
share: true
---

Flutter is a popular cross-platform framework for building mobile applications. It provides a rich set of UI components to create beautiful and responsive user interfaces. In this tutorial, we will explore how to create a WhatsApp-style chat UI using the `ListView` widget in Flutter.

## Getting started

To follow along with this tutorial, make sure you have Flutter installed on your system. If you haven't already, you can download Flutter from the official Flutter website and follow the installation instructions.

## Step 1: Setting up the project

Let's start by creating a new Flutter project. Open your terminal or command prompt and run the following command to create a new project:

```shell
flutter create whatsapp_chat_ui
```

Once the project is created, navigate to the project directory:

```shell
cd whatsapp_chat_ui
```

## Step 2: Creating the chat UI

Flutter provides the `ListView` widget to display a scrolling list of items. We'll use this widget to create the chat UI. Open the `lib/main.dart` file in your favorite code editor and replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(ChatApp());
}

class ChatApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Chat'),
        ),
        body: ListView.builder(
          itemBuilder: (BuildContext context, int index) {
            return ListTile(
              leading: CircleAvatar(
                backgroundImage: AssetImage('assets/user_avatar.png'),
              ),
              title: Text('John Doe'),
              subtitle: Text('Hello, how are you?'),
            );
          },
        ),
      ),
    );
  }
}
```

## Step 3: Adding chat messages

To make the chat UI more dynamic, let's add some chat messages to the list. Modify the `ListView.builder` as shown below:

```dart
body: ListView.builder(
  itemCount: _messages.length,
  itemBuilder: (BuildContext context, int index) {
    var message = _messages[index];
    return ListTile(
      leading: CircleAvatar(
        backgroundImage: AssetImage(message.avatar),
      ),
      title: Text(message.sender),
      subtitle: Text(message.text),
    );
  },
),
```

Here, `_messages` is a `List` of `Message` objects. You can define the `Message` class as follows:

```dart
class Message {
  final String avatar;
  final String sender;
  final String text;

  Message({this.avatar, this.sender, this.text});
}

List<Message> _messages = [
  Message(
    avatar: 'assets/user1_avatar.png',
    sender: 'John',
    text: 'Hello, how are you?',
  ),
  Message(
    avatar: 'assets/user2_avatar.png',
    sender: 'Jane',
    text: 'I\'m good, thanks!',
  ),
  // Add more messages as needed
];
```

Make sure to place the avatar images in the `assets` folder of your project.

## Step 4: Styling the chat UI

To make the chat UI look more like WhatsApp, you can add some styling. For example, you can modify the `ListTile` widget to display the sender's name and message as larger and bolder text:

```dart
ListTile(
  leading: CircleAvatar(
    backgroundImage: AssetImage(message.avatar),
  ),
  title: Text(
    message.sender,
    style: TextStyle(
      fontWeight: FontWeight.bold,
      fontSize: 16,
    ),
  ),
  subtitle: Text(
    message.text,
    style: TextStyle(
      fontSize: 14,
    ),
  ),
),
```

You can also customize the app bar by changing the background color, text color, etc.

## Conclusion

In this tutorial, you learned how to create a WhatsApp-style chat UI using the `ListView` widget in Flutter. You also learned how to add chat messages and style the UI to make it more appealing. Feel free to experiment with different styling options and customization to create your own unique chat UI.

#flutter #chatUI
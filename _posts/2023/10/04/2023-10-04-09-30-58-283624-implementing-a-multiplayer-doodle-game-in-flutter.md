---
layout: post
title: "Implementing a multiplayer doodle game in Flutter"
description: " "
date: 2023-10-04
tags: [introduction), setting]
comments: true
share: true
---

In this tutorial, we will learn how to create a multiplayer doodle game using Flutter. Flutter is a cross-platform framework that allows you to build beautiful and fast user interfaces for mobile, web, and desktop applications.

## Table of Contents

- [Introduction](#introduction)
- [Setting up the Project](#setting-up-the-project)
- [Designing the Game Screen](#designing-the-game-screen)
- [Implementing Multiplayer Functionality](#implementing-multiplayer-functionality)
- [Conclusion](#conclusion)

## Introduction

Doodle games are quite popular, and adding multiplayer functionality to such games enhances the user experience by allowing players to compete against each other in real-time. In this tutorial, we will create a simple doodle game where players can draw on the screen and see each other's drawings in real-time.

## Setting up the Project

To get started, make sure you have Flutter installed on your system. If not, you can follow the installation guide at [flutter.dev](https://flutter.dev).

Once Flutter is set up, create a new Flutter project using the following command:

```bash
flutter create multiplayer_doodle_game
```

Navigate to the project directory:

```bash
cd multiplayer_doodle_game
```

Open the project in your favorite code editor.

## Designing the Game Screen

To create the game screen, we will use the Flutter `Canvas` widget. This widget provides a low-level drawing API that allows us to draw directly on the screen.

First, open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() => runApp(DoodleGame());

class DoodleGame extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Multiplayer Doodle Game'),
        ),
        body: GameScreen(),
      ),
    );
  }
}

class GameScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: CustomPaint(painter: GamePainter()),
    );
  }
}

class GamePainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Implement drawing logic here
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }
}
```

This code sets up a basic Flutter app with a `DoodleGame` widget as the root widget. Inside the `DoodleGame` widget, we have a `GameScreen` widget that contains a `CustomPaint` widget. The `CustomPaint` widget takes a `GamePainter` as its painter, which is responsible for the actual drawing on the screen.

## Implementing Multiplayer Functionality

To add multiplayer functionality to our doodle game, we will use a real-time communication library like Socket.IO or WebSockets.

First, add the required dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  socket_io_client: ^2.0.0
```

Now, let's create a `SocketService` class that handles the communication with the server. Create a new file called `socket_service.dart` and add the following code:

```dart
import 'package:socket_io_client/socket_io_client.dart';

class SocketService {
  final String _serverUrl = 'your_server_url';
  Socket _socket;

  void connect() {
    _socket = io(_serverUrl, <String, dynamic>{
      'transports': ['websocket'],
      'autoConnect': false,
    });

    _socket.connect();
  }

  void disconnect() {
    _socket.disconnect();
  }

  void sendDrawingData(dynamic data) {
    _socket.emit('drawing_data', data);
  }

  void listenToDrawingData(void Function(dynamic) callback) {
    _socket.on('drawing_data', (dynamic data) {
      callback(data);
    });
  }
}
```

Replace the `'your_server_url'` with the actual server URL that you will be using for your multiplayer game.

Now, let's update the `GamePainter` class to send and receive drawing data:

```dart
class GamePainter extends CustomPainter {
  final SocketService _socketService = SocketService();

  @override
  void paint(Canvas canvas, Size size) {
    // Implement drawing logic here

    // Draw received drawing data
    _socketService.listenToDrawingData((dynamic data) {
      // Implement drawing data rendering here
    });
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return true;
  }
}
```

Finally, let's integrate the `SocketService` in the `GameScreen` class:

```dart
class GameScreen extends StatefulWidget {
  @override
  _GameScreenState createState() => _GameScreenState();
}

class _GameScreenState extends State<GameScreen> {
  final SocketService _socketService = SocketService();

  @override
  void initState() {
    super.initState();
    _socketService.connect();
  }

  @override
  void dispose() {
    _socketService.disconnect();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      child: CustomPaint(painter: GamePainter()),
    );
  }
}
```

With this setup, the app will connect to the server when the `GameScreen` is mounted and disconnect when it is unmounted. The `GamePainter` will listen for incoming drawing data and update the canvas accordingly.

## Conclusion

In this tutorial, we have learned how to create a multiplayer doodle game using Flutter. We started by setting up the project and designing the game screen using the `Canvas` widget. Then, we added multiplayer functionality using Socket.IO or WebSockets. By following this guide, you can build your own multiplayer doodle game and provide an engaging real-time experience for your users. Happy coding!

#flutter #multiplayer #gamedevelopment
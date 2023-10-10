---
layout: post
title: "Flutter command-based state management"
description: " "
date: 2023-10-10
tags: [state]
comments: true
share: true
---

State management is a crucial aspect of building robust and scalable applications in Flutter. There are several approaches to managing state in Flutter, and one popular method is command-based state management.

Command-based state management involves separating the state modification logic from the UI components. Instead of directly updating the state variables within the UI components, commands are used to modify the state. This approach provides better separation of concerns and improves code maintainability.

In this article, we will explore how to implement command-based state management in Flutter using the `provider` package.

## Getting Started

To get started with command-based state management in Flutter, we need to add the `provider` package to our project. Open your terminal and navigate to your project directory. Run the following command:

```bash
flutter pub add provider
```

This command will add the `provider` package to your `pubspec.yaml` file and download the package.

## Creating the Command

First, let's create a command that will be responsible for modifying the state. Create a new file called `counter_command.dart` and add the following code:

```dart
import 'dart:async';

class CounterCommand {
  // Stream controller to manage the commands
  final StreamController<void> _commandController = StreamController<void>();

  // Stream getter to expose the commands
  Stream<void> get commandStream => _commandController.stream;

  // Method to trigger the command
  void incrementCounter() {
    _commandController.add(null);
  }

  // Dispose method to close the stream
  void dispose() {
    _commandController.close();
  }
}
```

In the code above, we created a `CounterCommand` class that uses a `StreamController` to manage the commands. The `incrementCounter` method triggers the command by adding a value to the stream.

## Implementing the State

Next, let's create the state class that will be modified by the command. Create a new file called `counter_state.dart` and add the following code:

```dart
class CounterState {
  int counter;

  CounterState(this.counter);
}
```

In this simple example, we have a `CounterState` class that contains a counter variable. This state will be modified by the command.

## Consuming the State and Command

Now let's create a Flutter widget that will consume the state and command. Create a new file called `counter_widget.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

import 'counter_command.dart';
import 'counter_state.dart';

class CounterWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider<CounterState>(
      create: (_) => CounterState(0),
      child: Scaffold(
        appBar: AppBar(
          title: Text('Command-Based State Management'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Consumer<CounterState>(
                builder: (context, counterState, _) {
                  return Text(
                    'Counter: ${counterState.counter}',
                    style: TextStyle(fontSize: 24),
                  );
                },
              ),
              SizedBox(height: 16),
              Consumer<CounterCommand>(
                builder: (context, counterCommand, _) {
                  return ElevatedButton(
                    onPressed: counterCommand.incrementCounter,
                    child: Text('Increment Counter'),
                  );
                },
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

In the code above, we use the `ChangeNotifierProvider` widget from the `provider` package to provide the state to the widget tree. The `Consumer` widget is used to listen to the state changes and update the UI accordingly. The `Consumer` widget also listens to the command and triggers the specified method when the button is pressed.

## Wiring Everything Together

To wire everything together, open the `main.dart` file and make the following changes:

```dart
import 'package:flutter/material.dart';

import 'counter_widget.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Command-Based State Management',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: CounterWidget(),
    );
  }
}
```

Now you can run your application and see command-based state management in action. The counter value will be updated each time the increment button is pressed.

## Conclusion

Command-based state management provides an elegant and scalable solution for managing state in your Flutter applications. By separating the state modification logic from the UI components, you can enhance code maintainability and make your application more robust.

The `provider` package simplifies the implementation of command-based state management in Flutter. You can explore more advanced features of the `provider` package to handle more complex state management requirements.

Happy coding! #flutter #state-management
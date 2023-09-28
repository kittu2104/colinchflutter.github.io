---
layout: post
title: "Implementing dark mode in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [darkmode]
comments: true
share: true
---

With the increasing popularity of the dark mode feature in mobile applications, it has become essential for developers to provide their users with an option to switch between light and dark mode. In this blog post, we will explore how to implement dark mode in a StatelessWidget in Flutter.

## Setting Up the Project

Before we dive into the implementation, make sure you have a Flutter project set up. If you haven't done so already, you can create a new Flutter project by running the following command:

```dart
$ flutter create dark_mode_example
```

Navigate to the project directory:

```dart
$ cd dark_mode_example
```

## Adding Dependencies

To facilitate the implementation of dark mode, we will be using the `flutter_bloc` package. Open the `pubspec.yaml` file and add the following dependency:

```dart
dependencies:
  flutter_bloc: ^7.0.0
```

Save the file and run the command `flutter pub get`.

## Creating a Dark Mode Bloc

Let's start by creating a new file called `dark_mode_bloc.dart`. This file will contain the logic for managing the dark mode state.

```dart
import 'package:flutter_bloc/flutter_bloc.dart';

class DarkModeBloc extends Cubit<bool> {
  DarkModeBloc() : super(false);

  void toggleDarkMode(bool darkMode) => emit(darkMode);
}
```

In the code above, we define a `DarkModeBloc` class that extends `Cubit<bool>`. We initialize the initial state of dark mode as `false`. The `toggleDarkMode` method is used to update the dark mode state.

## Creating the User Interface

Next, let's create a new file called `dark_mode_screen.dart`. In this file, we'll define the `DarkModeScreen` widget, which will display the user interface and handle the toggling of dark mode.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

import 'dark_mode_bloc.dart';

class DarkModeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocBuilder<DarkModeBloc, bool>(
      builder: (context, darkMode) {
        return MaterialApp(
          theme: darkMode ? ThemeData.dark() : ThemeData.light(),
          home: Scaffold(
            appBar: AppBar(
              title: Text('Dark Mode Example'),
            ),
            body: Center(
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Text(
                    'Dark Mode:',
                    style: TextStyle(fontSize: 20),
                  ),
                  Switch(
                    value: darkMode,
                    onChanged: (value) {
                      context.read<DarkModeBloc>().toggleDarkMode(value);
                    },
                  ),
                ],
              ),
            ),
          ),
        );
      },
    );
  }
}
```

In the code above, we use the `BlocBuilder` widget from the `flutter_bloc` package to listen for state changes in the `DarkModeBloc`.  The current value of `darkMode` is used as the condition to determine the theme of the app. When the user toggles the `Switch` widget, we use the `context.read<DarkModeBloc>().toggleDarkMode(value)` method to update the state in the `DarkModeBloc`.

## Running the App

To run the app and test the dark mode feature, update the `lib/main.dart` file as follows:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

import 'dark_mode_bloc.dart';
import 'dark_mode_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Dark Mode Example',
      theme: ThemeData.light(),
      darkTheme: ThemeData.dark(),
      home: BlocProvider(
        create: (BuildContext context) => DarkModeBloc(),
        child: DarkModeScreen(),
      ),
    );
  }
}
```

Now, run the app using the command `flutter run` and observe the dark mode toggle switch in action.

## Conclusion

In this blog post, we learned how to implement dark mode in a `StatelessWidget` in Flutter using the `flutter_bloc` package. By using a `Cubit` to manage the dark mode state and toggling the theme based on this state, we can provide our users with an option to switch between light and dark mode in our Flutter applications.

#flutter #darkmode
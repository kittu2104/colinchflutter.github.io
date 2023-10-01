---
layout: post
title: "MediaQuery useDarkMode in Flutter"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

Dark mode has become increasingly popular in modern app design, as it provides a sleek and stylish look to user interfaces. Flutter, a cross-platform framework, offers several ways to implement dark mode in your app. One of these methods is by using the `MediaQuery` class, which allows you to access the current device's settings and provide a consistent user experience across different platforms.

In this tutorial, we will explore how to use `MediaQuery` to implement dark mode in your Flutter app. Let's get started!

## Step 1: Add Dependencies

To begin, make sure you have added the necessary dependencies in your `pubspec.yaml` file. The `provider` package is required to access the `MediaQuery` class.

```dart
dependencies:
  flutter:
    sdk: flutter
  provider: ^6.0.0
```

Don't forget to run `flutter pub get` to fetch the dependencies.

## Step 2: Initialize the Provider

The `provider` package allows us to manage the state of our app. We will use it to wrap our root `MaterialApp` and provide the dark mode state throughout the widget tree.

```dart
void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => DarkModeProvider(),
      child: MyApp(),
    ),
  );
}
```

In the above code, we wrap our `MyApp` widget with a `ChangeNotifierProvider`, which initializes our `DarkModeProvider` class.

## Step 3: Create the DarkModeProvider class

Let's create a new file called `dark_mode_provider.dart`. Then, define the `DarkModeProvider` class and add the necessary code to handle the dark mode state.

```dart
import 'package:flutter/material.dart';

class DarkModeProvider extends ChangeNotifier {
  bool _isDarkMode = false;

  bool get isDarkMode => _isDarkMode;

  void toggleDarkMode() {
    _isDarkMode = !_isDarkMode;
    notifyListeners();
  }

  ThemeData get themeData => _isDarkMode ? _darkTheme : _lightTheme;
  
  // Define your light theme
  static final ThemeData _lightTheme = ThemeData.light();
  
  // Define your dark theme
  static final ThemeData _darkTheme = ThemeData.dark();
}
```

The `DarkModeProvider` class provides a `toggleDarkMode` method to switch between light and dark modes. It also has a getter method `isDarkMode` to determine the current mode. Additionally, we define two `ThemeData` objects for the light and dark themes.

## Step 4: Use MediaQuery to Enable Dark Mode

Now let's use the `MediaQuery` class to enable dark mode based on the `isDarkMode` value provided by the `DarkModeProvider`.

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: Provider.of<DarkModeProvider>(context).themeData,
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final isDarkMode = Provider.of<DarkModeProvider>(context).isDarkMode;

    return Scaffold(
      appBar: AppBar(
        title: Text('Dark Mode Example'),
      ),
      body: Center(
        child: Text(
          'Dark Mode: ${isDarkMode ? 'Enabled' : 'Disabled'}',
          style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => Provider.of<DarkModeProvider>(context, listen: false).toggleDarkMode(),
        child: Icon(isDarkMode ? Icons.light_mode : Icons.dark_mode),
      ),
    );
  }
}
```

In the above example, we access the `themeData` from the `DarkModeProvider` and apply it to the `MaterialApp` theme. Inside `MyHomePage`, we retrieve the `isDarkMode` value and display it on the screen. Finally, we use a `FloatingActionButton` to toggle the dark mode using the `toggleDarkMode` method.

## Conclusion

By using `MediaQuery` and the `provider` package in Flutter, you can easily implement dark mode in your app. This gives users the option to customize their experience and enhances the overall aesthetics of your application.
---
layout: post
title: "Flutter dark mode state management"
description: " "
date: 2023-10-10
tags: [DarkMode]
comments: true
share: true
---

Dark mode has become a popular feature in many applications, including those built with Flutter. It offers a visually pleasing and energy-efficient alternative to the traditional light mode. In this blog post, we will explore different approaches to managing dark mode state in a Flutter application.

## Table of Contents
- [Introduction](#introduction)
- [Using Provider Package](#using-provider-package)
- [Using Riverpod Package](#using-riverpod-package)
- [Conclusion](#conclusion)

## Introduction

Before diving into the different state management approaches, let's first understand the concept of dark mode in Flutter. Dark mode refers to the color scheme of an application where the background color is dark and the text and UI elements are light in color. Flutter provides various ways to manage the state of dark mode, and we will explore two popular packages: Provider and Riverpod.

## Using Provider Package

Provider is a widely used state management package in the Flutter ecosystem. To enable dark mode state management using Provider, follow these steps:

1. Add the Provider dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  provider: ^6.0.0
```

2. Create a `ChangeNotifier` class to hold the state of dark mode. This class should extend the `ChangeNotifier` class from the provider package:

```dart
import 'package:flutter/material.dart';

class DarkModeNotifier extends ChangeNotifier {
  bool _isDarkModeEnabled = false;

  bool get isDarkModeEnabled => _isDarkModeEnabled;

  void toggleDarkMode(bool value) {
    _isDarkModeEnabled = value;
    notifyListeners();
  }
}
```

3. Wrap your top-level `MaterialApp` widget with the `ChangeNotifierProvider` and provide an instance of the `DarkModeNotifier`:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (_) => DarkModeNotifier(),
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      // Rest of your app code...
    );
  }
}
```

4. Access the dark mode state anywhere in your application using the `context.watch` or `context.select` method:

```dart
bool isDarkModeEnabled = context.watch<DarkModeNotifier>().isDarkModeEnabled;
```

5. Toggle the dark mode state by calling the `toggleDarkMode` method:

```dart
context.read<DarkModeNotifier>().toggleDarkMode(!isDarkModeEnabled);
```

## Using Riverpod Package

Riverpod is a state management package built on top of Provider. It offers a more modern and simplified approach to managing state in Flutter applications. To enable dark mode state management using Riverpod, follow these steps:

1. Add the Riverpod dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  riverpod: ^1.0.4
```

2. Create a `StateProvider` to hold the state of dark mode:

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

final darkModeProvider = StateProvider<bool>((ref) => false);
```

3. Wrap your top-level `MaterialApp` widget with the `ProviderScope` to provide access to the state:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

void main() {
  runApp(
    ProviderScope(
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      // Rest of your app code...
    );
  }
}
```

4. Access the dark mode state anywhere in your application using the `context.read` method:

```dart
bool isDarkModeEnabled = context.read(darkModeProvider).state;
```

5. Update the dark mode state by calling the `state` property and assigning it a new value:

```dart
context.read(darkModeProvider).state = !isDarkModeEnabled;
```

## Conclusion

Managing dark mode state in a Flutter application is crucial for providing an enhanced user experience. In this blog post, we explored two popular state management packages, Provider and Riverpod, to handle dark mode state. Remember to choose the package that best fits your project requirements and scale. Happy coding in both light and dark modes!

_#Flutter #DarkMode_
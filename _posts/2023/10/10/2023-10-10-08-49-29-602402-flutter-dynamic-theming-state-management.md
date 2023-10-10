---
layout: post
title: "Flutter dynamic theming state management"
description: " "
date: 2023-10-10
tags: [dynamictheming]
comments: true
share: true
---

When developing a Flutter application, one important aspect to consider is theming. Theming allows you to control the overall look and feel of your app, making it more visually appealing and consistent. In this blog post, we will explore how to implement dynamic theming and state management in Flutter.

## Table of Contents
1. [Introduction to Dynamic Theming](#introduction-to-dynamic-theming)
2. [State Management in Flutter](#state-management-in-flutter)
3. [Implementing Dynamic Theming with Provider](#implementing-dynamic-theming-with-provider)
4. [Conclusion](#conclusion)

## Introduction to Dynamic Theming

Dynamic theming enables users to switch between light and dark themes within the app. Instead of hardcoding the theme colors, dynamic theming allows you to reactively update the app's UI based on the selected theme.

## State Management in Flutter

State management is crucial in Flutter as it helps in managing the application's state and keeping the UI updated. There are various state management solutions available in Flutter, such as Provider, Riverpod, Bloc, and GetX.

One popular state management solution is `Provider`. Provider is a dependency injection system built specifically for Flutter. It allows you to easily share data across the widget tree and update the UI whenever there's a change in the data.

## Implementing Dynamic Theming with Provider

To implement dynamic theming with Provider, follow these steps:

1. Add the `provider` package to your `pubspec.yaml` file:
```yaml
dependencies:
  flutter:
    sdk: flutter
  provider: ^6.0.0
```

2. Create a `ThemeProvider` class that extends `ChangeNotifier`. This class will hold the current theme data:
```dart
import 'package:flutter/foundation.dart';
import 'package:flutter/material.dart';

class ThemeProvider extends ChangeNotifier {
  ThemeData _themeData = ThemeData.light();

  ThemeData get themeData => _themeData;

  void setThemeData(ThemeData themeData) {
    _themeData = themeData;
    notifyListeners();
  }
}
```

3. Wrap your `MaterialApp` with the `ChangeNotifierProvider` from the `provider` package. Provide an instance of the `ThemeProvider` class:
```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => ThemeProvider(),
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
       ...
    );
  }
}
```

4. In your UI widgets, use `Consumer` widget to access the current theme and update the UI accordingly:
```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final themeProvider = Provider.of<ThemeProvider>(context);

    return Scaffold(
      appBar: AppBar(
        title: Text('Dynamic Theming'),
      ),
      body: Center(
        child: Consumer<ThemeProvider>(
          builder: (context, themeProvider, child) {
            return Text(
              'Current theme: ${themeProvider.themeData.brightness == Brightness.dark ? 'Dark' : 'Light'}',
              style: TextStyle(
                fontSize: 20,
                fontWeight: FontWeight.bold,
              ),
            );
          },
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          if (themeProvider.themeData.brightness == Brightness.light) {
            themeProvider.setThemeData(ThemeData.dark());
          } else {
            themeProvider.setThemeData(ThemeData.light());
          }
        },
        child: Icon(Icons.brightness_4),
      ),
    );
  }
}
```

Now, when the `FloatingActionButton` is pressed, the theme will toggle between light and dark, and the UI will update accordingly.

## Conclusion

In this blog post, we explored how to implement dynamic theming and state management in Flutter using the `Provider` package. By leveraging Provider, we can easily switch between light and dark themes and keep the UI in sync with the selected theme. State management plays a key role in Flutter development, and using Provider simplifies the process of managing and updating the application's state.

#flutter #dynamictheming
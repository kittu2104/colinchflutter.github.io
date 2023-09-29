---
layout: post
title: "Using GetX for theme management in a Flutter app"
description: " "
date: 2023-09-29
tags: [flutter, GetX, theme]
comments: true
share: true
---

In this blog post, we will explore how to use the GetX package for theme management in a Flutter app. GetX is a lightweight, powerful, and easy-to-use state management library that provides various features like state management, dependency injection, and routing.

## Why Use GetX for Theme Management?

When developing a Flutter app, it is crucial to efficiently manage the app's theme to provide a consistent user experience. GetX offers a dedicated solution for managing themes, allowing us to easily switch between different themes at runtime and update the UI accordingly.

## Installation

To get started, add the `get` and `get_storage` dependencies to your Flutter project's `pubspec.yaml` file:

```dart
dependencies:
  flutter:
    sdk: flutter
  get: ^4.3.8
  get_storage: ^2.0.3
```

Then, run `flutter pub get` to fetch the dependencies.

## Theme Management with GetX

1. Create a new `ThemeController` class that extends `GetxController`:

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';
import 'package:get_storage/get_storage.dart';

class ThemeController extends GetxController {
  var isDarkMode = false.obs;

  @override
  void onInit() {
    // Retrieve the saved theme preference from GetStorage
    isDarkMode(GetStorage().read('isDarkMode') ?? false);
    super.onInit();
  }

  void toggleTheme() {
    // Toggle the current theme
    isDarkMode(!isDarkMode.value);
    // Save the updated theme preference using GetStorage
    GetStorage().write('isDarkMode', isDarkMode.value);
    // Update the app's theme
    Get.changeThemeMode(isDarkMode.value ? ThemeMode.dark : ThemeMode.light);
  }
}
```

2. Initialize the `ThemeController` in your app's `main.dart` file:

```dart
void main() async {
  await GetStorage.init();
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final ThemeController themeController = Get.put(ThemeController());

  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      title: 'My App',
      theme: ThemeData.light(),
      darkTheme: ThemeData.dark(),
      themeMode: themeController.isDarkMode.value ? ThemeMode.dark : ThemeMode.light,
      home: HomeScreen(),
    );
  }
}
```

3. Implement a UI widget that allows users to switch between themes:

```dart
class HomeScreen extends StatelessWidget {
  final ThemeController themeController = Get.find();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Switch(
              value: themeController.isDarkMode.value,
              onChanged: (value) {
                themeController.toggleTheme();
              },
            ),
            Text(
              themeController.isDarkMode.value ? 'Dark Mode' : 'Light Mode',
              style: TextStyle(
                fontWeight: FontWeight.bold,
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

4. That's it! You now have a fully functional theme management system using GetX in your Flutter app. Users can toggle between light and dark themes, and the app's UI will update accordingly.

## Conclusion

GetX provides an elegant and efficient way to handle theme management in Flutter apps. With its powerful state management capabilities, we can easily switch between different themes at runtime and update the UI accordingly. By using GetX for theme management, we can provide users with a consistent and customizable user experience.

#flutter #GetX #theme-management
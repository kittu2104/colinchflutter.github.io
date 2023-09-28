---
layout: post
title: "Handling user preferences with JSON serialization in Flutter"
description: " "
date: 2023-09-27
tags: [Flutter, JSONSerialization]
comments: true
share: true
---

When building a Flutter application, it's common to have user preferences that need to be stored and persisted across app sessions. One of the popular ways to handle user preferences in Flutter is by using JSON serialization.

JSON (JavaScript Object Notation) is a lightweight data interchange format that is easy for humans to read and write, and equally easy for machines to parse and generate. It provides a convenient way to represent complex data structures, including user preferences.

## Step 1: Defining the User Preferences Model

The first step is to define a model class that represents the user preferences. Let's say we want to store the user's theme preference and language preference. We can define a class called `UserPreferences` as follows:

```dart
class UserPreferences {
  final String theme;
  final String language;

  UserPreferences({required this.theme, required this.language});

  factory UserPreferences.fromJson(Map<String, dynamic> json) {
    return UserPreferences(
      theme: json['theme'],
      language: json['language'],
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'theme': theme,
      'language': language,
    };
  }
}
```

In the `UserPreferences` class, we have defined two properties `theme` and `language`, and also implemented the `fromJson` and `toJson` methods. These methods will be used for converting the user preferences to and from JSON format.

## Step 2: Storing and Retrieving User Preferences

To store and retrieve user preferences using JSON serialization, we can make use of the `shared_preferences` package in Flutter. This package provides a simple key-value storage system that can be used to store user preferences.

First, add the `shared_preferences` package to your `pubspec.yaml` file:

```yaml
dependencies:
  shared_preferences: ^2.0.6
```

Then, initialize the `SharedPreferences` instance and define methods to store and retrieve the user preferences:

```dart
import 'package:shared_preferences/shared_preferences.dart';

class PreferencesService {
  static const String _kUserPreferencesKey = 'user_preferences';

  SharedPreferences? _preferences;

  Future<void> init() async {
    _preferences = await SharedPreferences.getInstance();
  }

  UserPreferences getUserPreferences() {
    final jsonString = _preferences?.getString(_kUserPreferencesKey);
    if (jsonString != null) {
      return UserPreferences.fromJson(json.decode(jsonString));
    }
    // Return default preferences if no user preferences are stored
    return UserPreferences(theme: 'light', language: 'en');
  }

  Future<bool> saveUserPreferences(UserPreferences preferences) async {
    final jsonString = json.encode(preferences.toJson());
    return await _preferences?.setString(_kUserPreferencesKey, jsonString) ?? false;
  }
}
```

In the `PreferencesService` class, we initialize the `SharedPreferences` instance and provide methods to retrieve the user preferences using the `getUserPreferences()` method, as well as to save the user preferences using the `saveUserPreferences()` method.

## Step 3: Using User Preferences in the App

Once the `PreferencesService` class is set up, we can use it to handle the user preferences throughout the app. For example, to set the theme of the app based on the user preferences, we can use the following code snippet:

```dart
final preferences = PreferencesService();
await preferences.init();
final userPreferences = preferences.getUserPreferences();

if (userPreferences.theme == 'dark') {
  // Set app theme as dark
  // Your code here
} else {
  // Set app theme as light
  // Your code here
}
```

Similarly, you can use the user preferences to customize other aspects of your Flutter app, such as language settings, font sizes, and more.

## Conclusion

By using JSON serialization and the `shared_preferences` package, handling user preferences in a Flutter app becomes much easier and efficient. The `UserPreferences` model class allows for easy conversion to and from JSON, and the `PreferencesService` provides a convenient way to store and retrieve user preferences. Incorporating user preferences in your Flutter app enhances the user experience and customization options.

#Flutter #JSONSerialization
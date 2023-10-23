---
layout: post
title: "Storing and retrieving user preferences with MaterialApp."
description: " "
date: 2023-10-23
tags: [References]
comments: true
share: true
---
In mobile app development, it is common for users to have preferences that they want to save and retrieve across different sessions. These preferences can include settings like the app's theme, language, or any custom options specific to the app's functionality. In Flutter, we can use the MaterialApp widget and shared_preferences package to easily store and retrieve user preferences.

## Using the shared_preferences package 
The shared_preferences package provides a simple key-value store to persistently store data on the device. It supports various types of data, including bool, double, int, and String.

To use the shared_preferences package, we need to add it to the `pubspec.yaml` file in our Flutter project:

```yaml
dependencies:
  shared_preferences: ^2.0.5
```

Once the package is added, we need to import it in our Dart file:

```dart
import 'package:shared_preferences/shared_preferences.dart';
```

## Storing user preferences
Let's say we have an app where the user can choose between a light and dark theme. We can store the theme preference using shared_preferences. Here's an example of how we can do it:

```dart
void storeThemePreference(bool isDarkTheme) async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  prefs.setBool('isDarkTheme', isDarkTheme);
}
```

In this example, we use the `setBool()` method to store the value of the 'isDarkTheme' key.

## Retrieving user preferences
To retrieve the stored preference, we can use the `getBool()` method. Here's an example of how to retrieve the theme preference:

```dart
Future<bool> getThemePreference() async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  bool isDarkTheme = prefs.getBool('isDarkTheme') ?? false;
  return isDarkTheme;
}
```

In this example, we use the `getBool()` method to retrieve the boolean value stored for the 'isDarkTheme' key. If the value is not found, we return false as a default value.

## Using the preferences in MaterialApp
Once we have the user preference stored and retrieved, we can use it in the MaterialApp widget to set the theme dynamically. Here's an example:

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return FutureBuilder<bool>(
      future: getThemePreference(),
      builder: (BuildContext context, AsyncSnapshot<bool> snapshot) {
        if (snapshot.hasData && snapshot.data!) {
          return MaterialApp(
            theme: ThemeData.dark(),
            home: HomeScreen(),
          );
        } else {
          return MaterialApp(
            theme: ThemeData.light(),
            home: HomeScreen(),
          );
        }
      },
    );
  }
}
```

In this example, we use the `FutureBuilder` widget to asynchronously retrieve the theme preference. Based on the value returned, we set the theme of the MaterialApp widget accordingly.

## Conclusion
Storing and retrieving user preferences is an essential part of creating a personalized app experience. By using the shared_preferences package and the MaterialApp widget in Flutter, we can easily persist and use user preferences across different sessions. This allows users to have a consistent and customized experience with our app.

#References
- [shared_preferences package documentation](https://pub.dev/packages/shared_preferences)
- [Flutter documentation](https://flutter.dev/)
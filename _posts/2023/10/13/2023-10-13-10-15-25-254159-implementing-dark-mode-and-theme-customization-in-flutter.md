---
layout: post
title: "Implementing dark mode and theme customization in Flutter"
description: " "
date: 2023-10-13
tags: [theme, conclusion]
comments: true
share: true
---

In this tutorial, we will learn how to implement dark mode and theme customization in a Flutter app. Dark mode is a popular feature that allows users to switch the color scheme of the app to a darker theme, reducing eye strain and saving battery life on devices with OLED screens. Theme customization allows users to personalize the app's appearance by choosing their own color scheme.

## Table of Contents
1. [Understanding Themes in Flutter](#themes)
2. [Implementing Dark Mode](#dark-mode)
3. [Adding Theme Customization](#theme-customization)
4. [Conclusion](#conclusion)

## Understanding Themes in Flutter {#themes}

Themes in Flutter are a way to define the visual appearance of your app. They consist of a set of colors, fonts, and styles that can be applied to various widgets throughout your app. Flutter provides a default theme that is used if you don't explicitly specify a theme.

To implement dark mode and theme customization, we need to override the default theme and provide our own colors and styles.

## Implementing Dark Mode {#dark-mode}

To implement dark mode, we can define two themes - a light theme and a dark theme. The light theme will be the default theme, and the dark theme will be activated when the user enables dark mode.

First, let's create our light theme in the `main.dart` file:

```dart
final lightTheme = ThemeData(
  primaryColor: Colors.blue,
  // Add more theme properties here
);
```

Now, let's create the dark theme by extending the light theme and overriding the necessary properties:

```dart
final darkTheme = lightTheme.copyWith(
  brightness: Brightness.dark,
  // Override other theme properties for dark mode
);
```

To switch between the light and dark themes, we need to maintain the current theme state, usually using a state management solution like `Provider` or `Bloc`.

```dart
class ThemeProvider extends ChangeNotifier {
  bool isDarkMode = false;

  ThemeMode get currentTheme => isDarkMode ? ThemeMode.dark : ThemeMode.light;

  void toggleTheme() {
    isDarkMode = !isDarkMode;
    notifyListeners();
  }
}
```

Now, we can use the current theme in our app by wrapping it with a `ThemeProvider` and setting the `themeMode` property:

```dart
void main() {
  runApp(
    ChangeNotifierProvider<ThemeProvider>(
      create: (_) => ThemeProvider(),
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final themeProvider = Provider.of<ThemeProvider>(context);

    return MaterialApp(
      theme: lightTheme,
      darkTheme: darkTheme,
      themeMode: themeProvider.currentTheme,
      // Add your app routes and other properties here
    );
  }
}
```

Now, whenever the user enables dark mode, the app's theme will switch to the dark theme.

## Adding Theme Customization {#theme-customization}

To add theme customization, we need to provide options for the user to choose their own color scheme. This can be done using settings or preferences screens.

First, we need to define a set of custom colors that the user can choose from:

```dart
enum AppColors { red, blue, green, yellow }

Map<AppColors, Color> customColors = {
  AppColors.red: Colors.red,
  AppColors.blue: Colors.blue,
  AppColors.green: Colors.green,
  AppColors.yellow: Colors.yellow,
};
```

We can then update our `ThemeProvider` to include a property for the selected color:

```dart
class ThemeProvider extends ChangeNotifier {
  bool isDarkMode = false;
  AppColors selectedColor = AppColors.red;

  // ...
}
```

When the user changes the color preference, we can update the `selectedColor` property and notify listeners:

```dart
void changeColor(AppColors color) {
  selectedColor = color;
  notifyListeners();
}
```

Finally, we can use the selected color in our themes:

```dart
final lightTheme = ThemeData(
  primaryColor: customColors[selectedColor],
  // ...
);
```

## Conclusion {#conclusion}

Implementing dark mode and theme customization in Flutter allows users to personalize the appearance of your app. With the ability to switch between light and dark themes, as well as choose their own color scheme, users can have a more enjoyable and personalized experience with your app.
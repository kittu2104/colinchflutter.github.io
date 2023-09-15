---
layout: post
title: "State restoration for dark mode in Flutter apps"
description: " "
date: 2023-09-15
tags: [flutter, darkmode]
comments: true
share: true
---

With the increasing popularity of dark mode in mobile applications, it has become essential for developers to implement state restoration for the dark mode setting in their Flutter apps. State restoration allows the app to remember and restore the user's preference for dark mode, ensuring a consistent user experience across app launches.

In this blog post, we will explore how to implement state restoration for dark mode in Flutter apps, ensuring that the app remembers and restores the user's dark mode preference when the app is relaunched.

## The Approach

To implement state restoration for dark mode, we will leverage shared preferences, a popular package in Flutter that allows us to store key-value pairs persistently across app sessions.

Here's a step-by-step approach to implementing state restoration for dark mode:

1. **Add shared preferences to your project**: First, add the shared preferences package to your project by adding the following line to your `pubspec.yaml` file:

   ```yaml
   dependencies:
     shared_preferences: ^2.0.5
   ```

2. **Implement the dark mode toggle**: Implement the UI for the dark mode toggle switch in your app's settings or preferences screen. This toggle switch allows the user to enable or disable dark mode.

3. **Store the dark mode preference**: When the user toggles the dark mode switch, save their preference using shared preferences. Here's an example of how to do it:

   ```dart
   import 'package:shared_preferences/shared_preferences.dart';

   // Toggle switch callback
   void onDarkModeToggle(bool isDarkModeEnabled) async {
     SharedPreferences prefs = await SharedPreferences.getInstance();
     await prefs.setBool('darkMode', isDarkModeEnabled);
   }
   ```

4. **Restore the dark mode preference**: When the app starts, fetch the saved dark mode preference from shared preferences and apply it. Here's an example:

   ```dart
   void main() async {
     WidgetsFlutterBinding.ensureInitialized();
     SharedPreferences prefs = await SharedPreferences.getInstance();
     bool isDarkModeEnabled = prefs.getBool('darkMode') ?? false;  // Defaulting to false if preference not found

     runApp(MyApp(isDarkModeEnabled: isDarkModeEnabled));
   }

   class MyApp extends StatelessWidget {
     final bool isDarkModeEnabled;

     MyApp({required this.isDarkModeEnabled});

     @override
     Widget build(BuildContext context) {
       return MaterialApp(
         // Set the dark mode theme based on the preference
         theme: isDarkModeEnabled ? ThemeData.dark() : ThemeData.light(),
         home: MyHomePage(),
       );
     }
   }
   ```

## Conclusion

Implementing state restoration for dark mode in Flutter apps allows users to have a consistent experience between app launches. By leveraging shared preferences, we can easily store and retrieve the dark mode preference, providing a seamless experience to the users.

Remember to test the implementation thoroughly and consider adding a reset or default option for the dark mode setting in case the user wants to reset their preference.

#flutter #darkmode
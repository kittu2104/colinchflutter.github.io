---
layout: post
title: "Using localized strings in MaterialApp."
description: " "
date: 2023-10-23
tags: [Localization]
comments: true
share: true
---

The MaterialApp widget is a fundamental part of building Flutter apps. It provides a consistent, cohesive design for your app's UI. One important aspect of building user-friendly apps is supporting multiple languages. In this blog post, we will explore how to use localized strings in MaterialApp to support different languages.

## Table of Contents
- [Localization in Flutter](#Localization-in-Flutter)
- [Setting up translations](#Setting-up-translations)
- [Using localized strings in MaterialApp](#Using-localized-strings-in-MaterialApp)
- [Conclusion](#Conclusion)

## Localization in Flutter

Localization refers to the process of tailoring your app to different languages and regions. Flutter has built-in support for localization through the `intl` package. This package provides a way to define and use localized strings in your app.

## Setting up translations

To use localized strings in MaterialApp, you need to set up translations for different languages. Here are the steps to follow:

1. Add the `flutter_localizations` package to your `pubspec.yaml` file:
   ```yaml
   dependencies:
     flutter:
       sdk: flutter
     flutter_localizations:
       sdk: flutter
   ```

2. Import the necessary packages:
   ```dart
   import 'package:flutter/material.dart';
   import 'package:flutter_localizations/flutter_localizations.dart';
   ```

3. Define a `MaterialApp` widget and specify the supported locales and localization delegates:
   ```dart
   MaterialApp(
     localizationsDelegates: [
       GlobalMaterialLocalizations.delegate,
       GlobalWidgetsLocalizations.delegate,
     ],
     supportedLocales: [
       const Locale('en', 'US'), // English
       const Locale('es', 'ES'), // Spanish
       // Add more locales as needed
     ],
     // Rest of your app code
   )
   ```

4. Create a `messages` folder in the root of your project directory. Inside this folder, create a file for each supported language and define the corresponding localized strings. For example, create `messages_en_US.dart` for English and `messages_es_ES.dart` for Spanish:
   ```dart
   // messages_en_US.dart
   final Map<String, String> messages = {
     'title': 'Hello, World!',
     // Add more localized strings here
   };
   ```

5. In each language file, provide a method `initializeMessages()` to initialize the localized strings:
   ```dart
   // messages_en_US.dart
   Future<void> initializeMessages() async {
     final translation = await rootBundle.loadString('i18n/messages_en_US.json');
     final jsonTranslation = jsonDecode(translation) as Map<String, dynamic>;
     messages.addAll(jsonTranslation);
   }
   ```

6. Call `initializeMessages()` in your app's entry point (`main.dart`) before running the app:
   ```dart
   void main() async {
     await initializeMessages();
     runApp(MyApp());
   }
   ```

With the translations set up, you can now use localized strings in your MaterialApp.

## Using localized strings in MaterialApp

To use localized strings in MaterialApp, you can use the `localizationsDelegates` and `supportedLocales` properties. Here's an example:

```dart
MaterialApp(
  localizationsDelegates: [
    GlobalMaterialLocalizations.delegate,
    GlobalWidgetsLocalizations.delegate,
  ],
  supportedLocales: [
    const Locale('en', 'US'), // English
    const Locale('es', 'ES'), // Spanish
    // Add more locales as needed
  ],
  home: Scaffold(
    appBar: AppBar(
      title: Text(
        AppLocalizations.of(context).translate('title'),
      ),
    ),
    // Rest of your app code
  ),
)
```

In the above example, `AppLocalizations.of(context).translate('title')` translates the `title` key based on the current locale.

To fetch the translated string, you can use the following `AppLocalizations` class:

```dart
class AppLocalizations {
  final Locale locale;

  AppLocalizations(this.locale);

  static AppLocalizations of(BuildContext context) {
    return Localizations.of<AppLocalizations>(context, AppLocalizations);
  }

  String translate(String key) {
    // Look up the translated string based on the current locale
    return messages[key];
  }
}
```

Replace the `messages` map with the actual implementation of fetching the translated string based on the current locale.

## Conclusion

Using localized strings in MaterialApp is essential for creating a user-friendly app that supports multiple languages. By following the steps outlined in this blog post, you can easily set up translations and display localized content in your Flutter app. Happy coding!

*Tags: #Flutter #Localization*
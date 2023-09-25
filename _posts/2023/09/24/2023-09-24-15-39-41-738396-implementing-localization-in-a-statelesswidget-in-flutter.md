---
layout: post
title: "Implementing localization in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [Localization]
comments: true
share: true
---

Localization is an important aspect of mobile app development, especially when targeting an international audience. Flutter provides great support for localization, allowing you to easily create multilingual apps. In this blog post, we will explore how to implement localization in a `StatelessWidget` in Flutter.

## Step 1: Add Dependencies

First, we need to add the necessary dependencies to our `pubspec.yaml` file. Open the file and add the following lines:

```
dependencies:
  flutter_localizations:
    sdk: flutter
  intl: ^0.17.0
```

These dependencies are required for localization in Flutter.

## Step 2: Create Localization Files

Next, we need to create the localization files for each supported language. Create a new directory named `i18n` in the root of your Flutter project. Inside this directory, create separate files for each language, named according to their language code, e.g., `en.json`, `fr.json`, etc.

The content of each file should be a JSON dictionary with key-value pairs representing the localized strings. Here's an example for the English language file (`en.json`):

```json
{
  "title": "Hello World!",
  "subtitle": "Welcome to my app."
}
```

## Step 3: Load and Initialize Localization

In your `StatelessWidget`, import the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';
import 'package:intl/intl.dart';
import 'package:intl/intl_standalone.dart';
```

Create a class to handle the localization:

```dart
class AppLocalizations {
  final Locale locale;

  AppLocalizations(this.locale);

  static AppLocalizations? of(BuildContext context) {
    return Localizations.of<AppLocalizations>(context, AppLocalizations);
  }

  String getLocalizedString(String key) {
    return Intl.message(key, name: key, locale: locale.toString());
  }
}
```

Create a class to implement the localization delegate:

```dart
class AppLocalizationsDelegate extends LocalizationsDelegate<AppLocalizations> {
  const AppLocalizationsDelegate();

  @override
  bool isSupported(Locale locale) {
    return ['en', 'fr'].contains(locale.languageCode);
  }

  @override
  Future<AppLocalizations> load(Locale locale) {
    return SynchronousFuture<AppLocalizations>(AppLocalizations(locale));
  }

  @override
  bool shouldReload(AppLocalizationsDelegate old) => false;
}
```

## Step 4: Implement Localization in StatelessWidget

In your `StatelessWidget`, wrap the `MaterialApp` with the `Localizations` widget:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      localizationsDelegates: [
        const AppLocalizationsDelegate(),
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
      ],
      supportedLocales: [
        const Locale('en'),
        const Locale('fr'),
      ],
      home: HomeScreen(),
    );
  }
}
```

In the `HomeScreen` widget, you can now access the localized strings:

```dart
class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final localizations = AppLocalizations.of(context);

    return Scaffold(
      appBar: AppBar(
        title: Text(localizations!.getLocalizedString('title')),
      ),
      body: Center(
        child: Text(localizations!.getLocalizedString('subtitle')),
      ),
    );
  }
}
```

## Conclusion

Implementing localization in a `StatelessWidget` in Flutter is a straightforward process. By following the steps outlined in this blog post, you can easily create multilingual apps that cater to a global audience.

## #Localization #Flutter
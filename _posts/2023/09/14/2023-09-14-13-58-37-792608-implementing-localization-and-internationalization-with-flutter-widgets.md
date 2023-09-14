---
layout: post
title: "Implementing localization and internationalization with Flutter widgets"
description: " "
date: 2023-09-14
tags: [flutter, localization, internationalization]
comments: true
share: true
---

When developing mobile apps, it's important to consider the global audience and provide support for multiple languages and cultural adaptations. Flutter, with its powerful widget-based UI framework, makes implementing localization and internationalization a breeze. In this article, we will explore how to bring localization and internationalization to your Flutter app using Flutter widgets.

## Setup

Before we get started, make sure you have Flutter installed and a basic Flutter project set up.

## Step 1: Add Dependencies

Flutter provides a package called `flutter_localizations` that offers built-in support for localization and internationalization. To add this package, open your `pubspec.yaml` file and include the following line in the `dependencies` section:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
```

Save the file and run `flutter pub get` in your terminal to fetch the dependencies.

## Step 2: App Structure

To implement localization, create a new directory in your project called `l10n`. Inside this directory, create a file named `app_localizations.dart`. This file will contain the logic to load the localized strings.

```dart
class AppLocalizations {
  // TODO: Define your localized strings here
}
```

Next, create another directory called `localizations` parallel to the `l10n` directory. Inside the `localizations` directory, create a file named `app_localizations_delegate.dart`. This file will handle loading the correct localized strings based on the user's preferred locale.

```dart
import 'package:flutter/material.dart';
import 'package:flutter/foundation.dart';
import 'package: flutter_localizations/flutter_localizations.dart';

class AppLocalizationsDelegate extends LocalizationsDelegate<AppLocalizations> {
  const AppLocalizationsDelegate();

  @override
  bool isSupported(Locale locale) {
    return ['en', 'es'].contains(locale.languageCode);
  }

  @override
  Future<AppLocalizations> load(Locale locale) async {
    AppLocalizations localizations = AppLocalizations();
    await localizations.load(locale);
    return localizations;
  }

  @override
  bool shouldReload(AppLocalizationsDelegate old) => false;
}
```

## Step 3: Add Localization Support to the App

In the `main.dart` file, import the necessary files and modify the `MyApp` class as follows:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      localizationsDelegates: [
        AppLocalizationsDelegate(),
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
      ],
      supportedLocales: [
        const Locale('en'), // English
        const Locale('es'), // Spanish
      ],
      localeResolutionCallback: (Locale locale, Iterable<Locale> supportedLocales) {
        for (Locale supportedLocale in supportedLocales) {
          if (supportedLocale.languageCode == locale.languageCode) {
            return supportedLocale;
          }
        }
        return supportedLocales.first;
      },
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(AppLocalizations.of(context).yourLocalizedString),
      ),
      body: Center(
        child: Text(AppLocalizations.of(context).hello),
      ),
    );
  }
}
```

## Step 4: Loading the Localized Strings

Now let's fill in the `AppLocalizations` class with our localized strings. Modify the `app_localizations.dart` file as follows:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart' show rootBundle;
import 'dart:convert';

class AppLocalizations {
  Map<String, dynamic> _localizedStrings;

  Future load(Locale locale) async {
    String jsonString = await rootBundle.loadString('l10n/${locale.languageCode}.json');
    _localizedStrings = json.decode(jsonString);
  }

  String translate(String key) {
    return _localizedStrings[key];
  }

  static AppLocalizations of(BuildContext context) {
    return Localizations.of<AppLocalizations>(context, AppLocalizations);
  }
}
```

## Step 5: Create Localization String Files

Inside the `l10n` directory, create separate JSON files for each supported language. For example, create a file named `en.json` for English and `es.json` for Spanish. These files will contain the localized strings for each language.

```json
// en.json
{
  "hello": "Hello",
  "yourLocalizedString": "Your Localized String"
}

// es.json
{
  "hello": "Hola",
  "yourLocalizedString": "Tu cadena localizada"
}
```

That's it! You've successfully implemented localization and internationalization in your Flutter app using Flutter widgets. Now, when users switch their device's language settings, your app will automatically update to the appropriate localized strings.

Remember to use meaningful, SEO-friendly keywords in your localized strings to maximize the visibility of your app in different regions.

#flutter #localization #internationalization
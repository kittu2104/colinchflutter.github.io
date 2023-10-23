---
layout: post
title: "Internationalizing the app with MaterialApp."
description: " "
date: 2023-10-23
tags: [internationalization]
comments: true
share: true
---

When developing a mobile application, it's crucial to consider internationalization to cater to users from various linguistic backgrounds. Flutter provides built-in support for app internationalization through the `MaterialApp` widget.

## What is Internationalization?

Internationalization, also known as i18n, is the process of designing and developing software that can be adapted to multiple languages and cultures without requiring code changes.

## Internationalization in Flutter

In Flutter, internationalization is made easy with the help of the `MaterialApp` widget from the `flutter/material.dart` package. This widget allows us to define translations for various app components such as app name, button labels, error messages, and more.

To implement internationalization in your Flutter app, follow these steps:

### Step 1: Import the necessary packages

Import the `flutter_localizations` and `intl` packages in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_localizations:
    sdk: flutter
  intl: ^0.17.0
```

### Step 2: Create localization files

Create localization files for each language you want to support. These files should be placed under a `l10n` directory in your project.

For example, if you want to support English and Spanish, create the following files:

- `lib/l10n/app_en.arb` for English translations
- `lib/l10n/app_es.arb` for Spanish translations

### Step 3: Configure `MaterialApp`

In your `main.dart` file, configure the `MaterialApp` widget to enable internationalization. Add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';
import 'package:intl/intl.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      localizationsDelegates: [
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
      ],
      supportedLocales: [
        const Locale('en', ''), // English
        const Locale('es', ''), // Spanish
      ],
      title: 'My App',
      // other app configuration
      home: HomePage(),
    );
  }
}
```

### Step 4: Load translations

To load translations dynamically based on the user's device language, modify the `MyApp` widget as follows:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      localizationsDelegates: [
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
        AppLocalizations.delegate,
      ],
      supportedLocales: [
        const Locale('en', ''),
        const Locale('es', ''),
      ],
      localeResolutionCallback: (locale, supportedLocales) {
        // Use the default locale ('en') if the device locale is not supported
        if (supportedLocales.contains(locale)) {
          return locale;
        } else {
          return const Locale('en', '');
        }
      },
      title: 'My App',
      // other app configuration
      home: HomePage(),
    );
  }
}
```

### Step 5: Utilize translations

Once the setup is complete, you can utilize the translations in your app. Flutter provides the `intl` package to handle localization.

For example, if you want to display a localized app title, use the `AppLocalizations.of(context).title` method:

```dart
import 'package:flutter/material.dart';
import 'package:intl/intl.dart';
import 'l10n/app_localizations.dart';

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(AppLocalizations.of(context).title),
      ),
      // other widget tree
    );
  }
}
```

## Conclusion

By leveraging the `MaterialApp` widget and the `intl` package, it becomes effortless to internationalize your Flutter app. Users from different language backgrounds will appreciate the ability to use your app in their native language, enhancing the overall user experience.

#flutter #internationalization
---
layout: post
title: "Implementing multi-language support in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [localization]
comments: true
share: true
---

Flutter is a popular framework for building cross-platform mobile applications. To make your app accessible to a wider audience, it's important to provide multi-language support. In this blog post, we'll explore how to implement multi-language support in a `StatelessWidget` in Flutter.

## Step 1: Setup

First, let's add the `flutter_localizations` package to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
```

After adding the package, run `flutter pub get` to fetch the dependencies.

## Step 2: Create internationalization files
Next, create a new folder in your project root called `l10n`. Inside the `l10n` folder, create a new file for each language you want to support, following the naming convention `intl_<language_code>.arb`. For example, for English (US), create a file named `intl_en.arb`.

The `.arb` files should contain key-value pairs for each string you want to translate. Here's an example:

```json
{
  "app_title": "My Flutter App",
  "welcome_message": "Welcome to my app!"
}
```

## Step 3: Generate translation files

To generate the translation files based on the `.arb` files, run the following command in the terminal:

```bash
flutter pub run flutter_localizations:generate
```

This command will create a `l10n.dart` file inside the `lib` directory.

## Step 4: Implement language delegate

In your `l10n.dart` file, implement a `LocalizationsDelegate` class that loads the translations based on the user's locale. Here's an example:

```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:flutter/services.dart' show rootBundle;

class AppLocalizations {
  final Locale locale;

  AppLocalizations(this.locale);

  static AppLocalizations? of(BuildContext context) {
    return Localizations.of<AppLocalizations>(context, AppLocalizations);
  }

  late Map<String, String> _localizedStrings;

  Future<bool> load() async {
    String jsonString = await rootBundle.loadString('assets/i18n/intl_${locale.languageCode}.json');
    Map<String, dynamic> jsonMap = json.decode(jsonString);
    _localizedStrings = jsonMap.map((key, value) => MapEntry(key, value.toString()));
    return true;
  }

  String translate(String key) {
    return _localizedStrings[key] ?? key;
  }
}

class AppLocalizationsDelegate extends LocalizationsDelegate<AppLocalizations> {
  final List<Locale> supportedLocales;

  const AppLocalizationsDelegate(this.supportedLocales);

  @override
  bool isSupported(Locale locale) => supportedLocales.contains(locale);

  @override
  Future<AppLocalizations> load(Locale locale) async {
    AppLocalizations localizations = AppLocalizations(locale);
    await localizations.load();
    return localizations;
  }

  @override
  bool shouldReload(AppLocalizationsDelegate old) => false;
}
```

## Step 5: Wrap your app with `Localizations`

In your `main.dart` file, wrap your `WidgetApp` with the `Localizations` widget and provide the supported locales and the delegate. Here's an example:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      localizationsDelegates: [
        const AppLocalizationsDelegate([
          Locale('en', ''),
          Locale('fr', ''),
          // Add more supported locales here
        ]),
      ],
      onGenerateTitle: (BuildContext context) => AppLocalizations.of(context)!.translate('app_title'),
      home: MyHomePage(),
    );
  }
}

void main() {
  runApp(MyApp());
}
```

## Conclusion

By following these steps, you can easily implement multi-language support in a `StatelessWidget` in Flutter. This will help you cater to users from different language backgrounds and make your app more accessible. Start translating your app now and target a larger global audience!

#flutter #localization
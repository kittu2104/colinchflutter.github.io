---
layout: post
title: "Flutter localization state management"
description: " "
date: 2023-10-10
tags: [localization]
comments: true
share: true
---

Localization is a crucial aspect of any mobile application as it allows developers to support multiple languages and adapt to different regions. In Flutter, localization can be achieved using the `flutter_localizations` package, which provides support for internationalization.

When it comes to managing the state for localization in Flutter, using a state management approach is essential. In this blog post, we will explore how to manage localization state using the Provider package in Flutter.

## Table of Contents
- [Setting up the Project](#setting-up-the-project)
- [State Management using Provider](#state-management-using-provider)
- [Localizing the App](#localizing-the-app)
- [Conclusion](#conclusion)

## Setting up the Project

To get started, create a new Flutter project:

```bash
flutter create flutter_localization_example
cd flutter_localization_example
```

Next, add the 'provider' dependency to your project's `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  provider: ^6.0.0
```

Run `flutter pub get` in the terminal to fetch the dependency.

## State Management using Provider

Provider is a popular state management package in Flutter that simplifies the process of managing state across the application. To use Provider for localization, first create a new Dart file called `localization_provider.dart`. 

In this file, define a class `LocalizationProvider` that extends `ChangeNotifier` and implements the logic for managing the app's localization state:

```dart
import 'package:flutter/foundation.dart';

class LocalizationProvider extends ChangeNotifier {
  Locale _locale;

  Locale get locale => _locale;

  void setLocale(Locale locale) {
    _locale = locale;
    notifyListeners();
  }
}
```

The `LocalizationProvider` class holds the current locale and provides a method, `setLocale`, to update the locale. By inheriting from `ChangeNotifier`, any changes to the locale will notify the listeners.

## Localizing the App

Now that we have set up the state management using Provider, let's proceed to localize our app. The first step is to define the supported locales in our application. Create a new Dart file called `app_localizations.dart`. 

In the `AppLocalizations` class, define the `supportedLocales` property and a simple constructor:

```dart
import 'package:flutter/material.dart';

class AppLocalizations {
  final Locale locale;

  AppLocalizations(this.locale);

  static AppLocalizations of(BuildContext context) {
    return Localizations.of<AppLocalizations>(context, AppLocalizations);
  }

  static Map<String, Map<String, String>> _localizedValues = {
    'en': {
      'title': 'Flutter Localization Example',
      'welcome': 'Welcome!',
      'message': 'Hello, from AppLocalizations!',
    },
    'fr': {
      'title': 'Exemple de localisation Flutter',
      'welcome': 'Bienvenue !',
      'message': 'Bonjour, depuis AppLocalizations !',
    },
  };

  String get title => _localizedValues[locale.languageCode]['title'];
  String get welcome => _localizedValues[locale.languageCode]['welcome'];
  String get message => _localizedValues[locale.languageCode]['message'];
}
```

In the `_localizedValues` map, we define the localized strings for each supported locale. The `of` method allows us to access the `AppLocalizations` instance from the Flutter's `Localization` object, which we will set up next.

To set up the localization in our app, open the `main.dart` file and modify the `main` method:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';
import 'package:flutter_localization_example/localization_provider.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final LocalizationProvider provider = LocalizationProvider();

  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (_) => provider,
      child: Consumer<LocalizationProvider>(
        builder: (context, model, child) {
          return MaterialApp(
            title: 'Localization Example',
            theme: ThemeData(
              primarySwatch: Colors.blue,
            ),
            locale: model.locale,
            supportedLocales: [
              Locale('en', ''),
              Locale('fr', ''),
            ],
            localizationsDelegates: [
              AppLocalizations.delegate,
              GlobalMaterialLocalizations.delegate,
              GlobalWidgetsLocalizations.delegate,
            ],
            home: MyHomePage(),
          );
        },
      ),
    );
  }
}
```

Here, we wrap the `MaterialApp` with `ChangeNotifierProvider` and `Consumer` widgets to provide the `LocalizationProvider` to the child widgets. We set the `locale` property of `MaterialApp` using the provider's `locale` value.

## Conclusion

In this blog post, we explored how to manage the localization state in Flutter using the Provider package. We created a `LocalizationProvider` class to handle the locale state and use the `provider` package to manage the state. By using this approach, we can easily switch between different locales in our Flutter app. You can find the complete example code on [GitHub](https://github.com/example/flutter_localization_example).

#flutter #localization
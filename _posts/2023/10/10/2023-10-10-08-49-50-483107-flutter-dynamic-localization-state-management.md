---
layout: post
title: "Flutter dynamic localization state management"
description: " "
date: 2023-10-10
tags: [localization]
comments: true
share: true
---

When developing Flutter apps, internationalization and localization are essential to ensure your app can be used by users from different regions and languages. Flutter provides built-in support for localization, and managing the localization state can be done in various ways. In this blog post, we will explore how to handle dynamic localization state management in Flutter.

## Table of Contents
- [Introduction to Localization in Flutter](#introduction-to-localization-in-flutter)
- [State Management Options](#state-management-options)
- [Using Provider for Dynamic Localization](#using-provider-for-dynamic-localization)
- [Implementing Dynamic Localization](#implementing-dynamic-localization)
- [Final Thoughts](#final-thoughts)

## Introduction to Localization in Flutter

Localization refers to adapting your app to different languages, cultures, and regions. Flutter provides the `flutter_localizations` package, which offers tools and APIs to handle localization in your app. It allows you to define localized resources and easily switch between different locales at runtime.

## State Management Options

When it comes to managing the localization state in Flutter, you have different options, including:

- **InheritedWidget**: Flutter's built-in mechanism for sharing data across the widget tree.
- **Provider**: An easy-to-use state management solution that simplifies passing the localization state to the widgets.
- **Bloc**: A more advanced state management pattern that can be used for managing complex application states.

In this blog post, we will focus on using the Provider package for dynamic localization state management.

## Using Provider for Dynamic Localization

Provider is a popular state management solution in the Flutter community. It allows you to easily share data between widgets and update the UI when the data changes. To use Provider for dynamic localization, follow these steps:

1. Add the `provider` package to your `pubspec.yaml` file:

    ```yaml
    dependencies:
      flutter:
        sdk: flutter
      provider: ^5.0.0
    ```

2. Import the necessary packages in your Dart file:

    ```dart
    import 'package:flutter/material.dart';
    import 'package:provider/provider.dart';
    import 'package:flutter_localizations/flutter_localizations.dart';
    ```

3. Create a class to hold the localization state:

    ```dart
    class LocalizationNotifier extends ChangeNotifier {
      Locale _locale = Locale('en');

      Locale get locale => _locale;

      void setLocale(Locale newLocale) {
        _locale = newLocale;
        notifyListeners();
      }
    }
    ```

4. Wrap your `MaterialApp` or `CupertinoApp` widget with `ChangeNotifierProvider`:

    ```dart
    void main() {
      runApp(
        ChangeNotifierProvider(
          create: (_) => LocalizationNotifier(),
          child: MyApp(),
        ),
      );
    }
    ```

5. Access the localization state using `Provider.of` or `Consumer`:

    ```dart
    class MyApp extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        final localization = Provider.of<LocalizationNotifier>(context);

        return MaterialApp(
          ...
          localizationsDelegates: [
            GlobalMaterialLocalizations.delegate,
            GlobalWidgetsLocalizations.delegate,
          ],
          supportedLocales: [
            Locale('en', 'US'),
            Locale('es', 'ES'),
            // Add more supported locales
          ],
          locale: localization.locale,
          ...
        );
      }
    }
    ```

6. Update the localization state when the locale changes:

    ```dart
    class LanguageSelector extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        final localization = Provider.of<LocalizationNotifier>(context);

        return DropdownButton<Locale>(
          value: localization.locale,
          onChanged: (newLocale) {
            localization.setLocale(newLocale);
          },
          items: [
            DropdownMenuItem(
              value: Locale('en', 'US'),
              child: Text('English'),
            ),
            DropdownMenuItem(
              value: Locale('es', 'ES'),
              child: Text('Español'),
            ),
            // Add more supported locales
          ],
        );
      }
    }
    ```

## Implementing Dynamic Localization

To implement dynamic localization with Provider, follow these steps:

1. Create a `LocalizationsDelegate` for your app's localized resources:

    ```dart
    class AppLocalizationsDelegate extends LocalizationsDelegate<AppLocalizations> {
      @override
      bool isSupported(Locale locale) {
        return ['en', 'es'].contains(locale.languageCode);
      }

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

2. Create a class to hold your app's localized strings:

    ```dart
    class AppLocalizations {
      Locale locale;
      Map<String, String> localizedStrings;

      AppLocalizations(this.locale);

      Future<void> load() async {
        String jsonStrings =
            await rootBundle.loadString('assets/i18n/${locale.languageCode}.json');
        Map<String, dynamic> decodedStrings = json.decode(jsonStrings);
        localizedStrings = decodedStrings.map((key, value) => MapEntry(key, value.toString()));
      }

      String translate(String key) {
        return localizedStrings[key];
      }

      static AppLocalizations of(BuildContext context) {
        return Localizations.of<AppLocalizations>(context, AppLocalizations);
      }
    }
    ```

3. Wrap your app's root widget with `MaterialApp` or `CupertinoApp`:

    ```dart
    MaterialApp(
      ...
      localizationsDelegates: [
        AppLocalizationsDelegate(), // Add your custom delegate
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
      ],
      supportedLocales: [
        Locale('en', 'US'),
        Locale('es', 'ES'),
        // Add more supported locales
      ],
      locale: localization.locale,
      ...
    )
    ```

With these steps, your Flutter app will now be able to dynamically switch between different locales based on user selection.

## Final Thoughts

Managing the localization state dynamically is crucial for providing a seamless internationalization experience in your Flutter apps. In this blog post, we explored using the Provider package to handle the localization state management. By following the steps outlined above, you will be able to implement dynamic localization in your Flutter app with ease.

Have you tried dynamic localization with Provider in your Flutter apps? Share your experience in the comments!

#flutter #localization
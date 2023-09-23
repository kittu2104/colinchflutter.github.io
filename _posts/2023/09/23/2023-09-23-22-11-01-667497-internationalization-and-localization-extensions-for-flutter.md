---
layout: post
title: "Internationalization and localization extensions for Flutter"
description: " "
date: 2023-09-23
tags: [flutter, localization]
comments: true
share: true
---

Flutter is an open-source framework developed by Google that allows developers to build cross-platform applications with ease. One of the key aspects of creating successful mobile applications is the ability to support multiple languages and cater to different regions. In this blog post, we will explore some of the popular internationalization and localization extensions available for Flutter.

## 1. flutter_localizations

Flutter provides a built-in package called `flutter_localizations` that allows developers to add internationalization and localization support to their Flutter applications. This package provides localization support for various aspects of an application, such as text, dates, numbers, and currencies.

To use `flutter_localizations`, you first need to add it as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
```

After adding the dependency, you can import the package and specify the supported locales in your application. You can define the supported locales in the `MaterialApp` widget using the `supportedLocales` parameter:

```dart
import 'package:flutter_localizations/flutter_localizations.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My App',
      supportedLocales: [
        const Locale('en'), // English
        const Locale('es'), // Spanish
        const Locale('fr'), // French
      ],
      localizationsDelegates: [
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
      ],
      home: MyHomePage(),
    );
  }
}
```

Once you have set up the supported locales, you can use the `Localizations` widget to retrieve the localized strings based on the device language:

```dart
Text(AppLocalizations.of(context).hello);
```

In this example, `AppLocalizations` is a class that provides the localized strings for different languages. You can define this class and the corresponding localized strings in separate files.

## 2. easy_localization

Another popular internationalization and localization extension for Flutter is `easy_localization`. This package simplifies the process of managing translations and provides additional features like pluralization and gender-specific translations.

To use `easy_localization`, you need to add it as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  easy_localization: ^3.0.0
```

After adding the dependency, you need to initialize `easy_localization` in your `main.dart` file:

```dart
import 'package:easy_localization/easy_localization.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await EasyLocalization.ensureInitialized();
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return EasyLocalization(
      supportedLocales: [
        Locale('en', 'US'), // English
        Locale('es', 'ES'), // Spanish
        Locale('fr', 'FR'), // French
      ],
      path: 'assets/translations', // Path to the translations files
      fallbackLocale: Locale('en', 'US'), // Fallback locale
      child: MaterialApp(
        title: 'My App',
        localizationsDelegates: context.localizationDelegates,
        supportedLocales: context.supportedLocales,
        locale: context.locale,
        home: MyHomePage(),
      ),
    );
  }
}
```

Once you have set up `easy_localization`, you can use the `tr` function to retrieve the localized strings:

```dart
Text(tr('hello'));
```

In this example, `tr` is a function provided by `easy_localization` that fetches the corresponding translation based on the device language.

## Conclusion

Supporting internationalization and localization in Flutter applications is crucial for reaching a wider audience and delivering a personalized user experience. The `flutter_localizations` and `easy_localization` extensions make it easier to implement multilingual support in your applications. Choose the one that best fits your requirements and start building applications that cater to users worldwide.

#flutter #localization
---
layout: post
title: "Internationalization and localization in Flutter SSR"
description: " "
date: 2023-09-21
tags: [flutterSSR, internationalization, localization]
comments: true
share: true
---

Internationalization (i18n) and Localization (l10n) are important aspects of app development and are crucial for creating applications that can be easily adapted to different languages, cultures, and regions. In this blog post, we will explore how to implement internationalization and localization in Flutter SSR (Server Side Rendering) applications.

## What is Internationalization and Localization?

- **Internationalization**: It is the process of designing and developing an application in a way that it can support multiple languages, without the need for code changes. It involves preparing the app to be easily translated into different languages.

- **Localization**: It is the process of adapting an application to a specific language, region, or culture by translating the app's content, date formats, number formats, and other language-dependent aspects.

## Internationalization and Localization in Flutter SSR

Flutter provides built-in support for internationalization and localization, making it easy to create apps that can be easily translated and localized. However, the process is slightly different when it comes to Flutter SSR applications. Let's see how to achieve internationalization and localization in Flutter SSR.

## Step 1: Add Localization Dependencies

To start with, we need to add the following localization dependencies in your `pubspec.yaml` file:

```yaml
dev_dependencies:
  flutter_localizations:
    sdk: flutter
  flutter_gen:
    sdk: flutter
```

- `flutter_localizations` provides support for localization in Flutter apps.
- `flutter_gen` generates the required localization files.

## Step 2: Generate Localization Files

Next, we need to generate the localization files containing the translations for the app's content. Flutter SSR uses `arb` (Application Resource Bundle) files to store the translations.

To generate the localization files, run the following command in the terminal:

```bash
flutter gen-l10n
```

This command will generate the required `l10n.dart` file and the `intl_messages.arb` file.

## Step 3: Create Localization Delegate

In your Flutter SSR application code, create a `LocalizationDelegate` class that extends `LocalizationsDelegate`. This class will be responsible for loading the translations and providing them to the app.

```dart
class SSRLocalizationDelegate extends LocalizationsDelegate<SSRLocalizations> {
  @override
  bool isSupported(Locale locale) {
    return SSRAppLocalizations.supportedLocales.contains(locale);
  }

  @override
  Future<SSRLocalizations> load(Locale locale) async {
    final loc = SSRLocalizations(locale);
    await loc.load();
    return loc;
  }

  @override
  bool shouldReload(LocalizationsDelegate<SSRLocalizations> old) => false;
}
```

## Step 4: Implement Localization Widget

Create a `Localization` widget that wraps your Flutter SSR app and provides the translations to the app's widgets.

```dart
class Localization extends StatelessWidget {
  final Widget child;

  Localization({required this.child});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Localizations(
        delegates: [
          SSRLocalizationDelegate(),
          GlobalMaterialLocalizations.delegate,
          GlobalWidgetsLocalizations.delegate,
        ],
        locale: Locale('en'),
        child: child,
      ),
    );
  }
}
```

Here, we provide the `SSRLocalizationDelegate` along with the `GlobalMaterialLocalizations` and `GlobalWidgetsLocalizations` delegates, which handle material design and widget translations.

## Step 5: Localize the App

Now, we can start localizing our Flutter SSR app. In each widget that needs to display localized content, wrap the relevant text strings with the `SSRLocalizations.of(context)` method, and specify the desired translation key.

```dart
Text(SSRLocalizations.of(context).helloWorld),
```

## Conclusion

In this blog post, we learned how to implement internationalization and localization in Flutter SSR applications. By following these steps, you can easily create apps that can be adapted to different languages and regions. Make sure to generate the localization files, create a localization delegate, implement the localization widget, and localize the relevant app content.

#flutterSSR #internationalization #localization
---
layout: post
title: "Implementing text localization in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [flutter, localization]
comments: true
share: true
---

Localization is a crucial aspect of building a multilingual app. It allows users to view content in their preferred language, thereby enhancing the user experience. In this tutorial, we will learn how to implement text localization in a `StatelessWidget` in Flutter.

## Adding Localization Support

To support localization in Flutter, we need to add the `flutter_localizations` package to our project dependencies. Open the `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter_localizations:
    sdk: flutter
```

Now, let's update the packages by running the following command:

```
flutter packages get
```

## Creating Localization Files

Next, we need to create localization files for each language we want to support. Create a folder called `lang` in the root directory of your Flutter project. Inside the `lang` folder, create a file for each language using the ISO 639-1 language code as the file name. For example, `en.json` for English, `es.json` for Spanish, and so on.

The structure of each localization file should follow the JSON format. Here's an example for English localization:

```json
{
  "hello": "Hello",
  "welcome": "Welcome to Flutter"
}
```

Create the necessary localization files for the languages you want to support.

## Implementing Localization logic

Inside your `StatelessWidget`, we need to implement the logic to fetch the localized strings and display them. Let's create a new `_AppLocalizations` class that extends `LocalizationsDelegate`:

```dart
class _AppLocalizations {
  final Locale locale;

  _AppLocalizations(this.locale);

  static Map<String, String> _localizedStrings;

  Future<bool> load() async {
    String jsonContent =
        await rootBundle.loadString('lang/${locale.languageCode}.json');

    Map<String, dynamic> jsonMap = json.decode(jsonContent);

    _localizedStrings = jsonMap.map((key, value) {
      return MapEntry(key, value.toString());
    });

    return true;
  }

  String translate(String key) {
    return _localizedStrings[key];
  }

  static _AppLocalizations of(BuildContext context) {
    return Localizations.of<_AppLocalizations>(context, _AppLocalizations);
  }
}
```

In the code above, we load the appropriate language file based on the locale and store the localized strings in a map. The `translate` function retrieves the value associated with the given `key` from the map.

## Building the UI

Let's now update the UI to display the localized strings. Wrap the root widget of your `StatelessWidget` with a `Localizations` widget:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My App',
      localizationsDelegates: [
        _AppLocalizationsDelegate(), // Custom delegate
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
      ],
      supportedLocales: [
        Locale('en', 'US'), // English
        Locale('es', 'ES'), // Spanish
      ],
      home: MyHomePage(),
    );
  }
}
```

Here, we added our custom localization delegate, `_AppLocalizationsDelegate()`, as well as the default Flutter delegates for material and widgets localization.

Now, to display a localized string, use the `translate` method we defined earlier:

```dart
class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final localizedStrings = _AppLocalizations.of(context);

    return Scaffold(
      appBar: AppBar(
        title: Text(localizedStrings.translate('hello')),
      ),
      body: Center(
        child: Text(
          localizedStrings.translate('welcome'),
          style: TextStyle(fontSize: 20),
        ),
      ),
    );
  }
}
```

## Conclusion

In this tutorial, we learned how to implement text localization in a `StatelessWidget` in Flutter. By leveraging the `flutter_localizations` package and following the steps outlined here, you can easily add support for multiple languages in your Flutter applications.

#flutter #localization
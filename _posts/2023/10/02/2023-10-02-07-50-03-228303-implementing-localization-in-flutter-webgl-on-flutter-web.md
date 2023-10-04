---
layout: post
title: "Implementing localization in Flutter WebGL on Flutter Web"
description: " "
date: 2023-10-02
tags: [WebGL, Localization]
comments: true
share: true
---

Flutter is an open-source UI toolkit developed by Google, which allows developers to build native-like applications for multiple platforms. It provides a rich set of features, including support for localization, making it easy to create apps that can be easily translated into multiple languages.

Localization is the process of adapting an application to different languages and cultures. In this article, we will explore how to implement localization in Flutter when targeting the web using Flutter WebGL.

### Step 1: Setting up the project

To get started, ensure you have the latest version of Flutter installed on your machine. Create a new Flutter project using the following command:

```dart
flutter create my_project
```

Once the project is created, navigate to the project directory:

```dart
cd my_project
```

Next, enable web support for the project:

```dart
flutter config --enable-web
```

This will enable Flutter web support in your project.

### Step 2: Adding localization dependencies

To enable localization in your Flutter project, you need to add the `flutter_localizations` package to your `pubspec.yaml` file. Open the `pubspec.yaml` file and add the following line under the `dependencies` section:

```dart
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
```

Save the `pubspec.yaml` file and run the following command to download the dependencies:

```dart
flutter packages get
```

This will download the required dependencies for localization.

### Step 3: Adding localization files

Create a new directory called `l10n` in the root of your project. This directory will contain the localization files for different languages.

Inside the `l10n` directory, create a new file called `app_localizations.dart`. This file will contain the logic for loading the localized strings.

Copy the following code into the `app_localizations.dart` file:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/foundation.dart';
import 'package:intl/intl.dart';

/// Localizations class that loads the localized strings
class AppLocalizations {
  final Locale locale;

  AppLocalizations(this.locale);

  static AppLocalizations? of(BuildContext context) {
    return Localizations.of<AppLocalizations>(context, AppLocalizations);
  }

  static final Map<String, Map<String, String>> _localizedValues = {
    'en': {
      'title': 'Hello World',
    },
    'fr': {
      'title': 'Bonjour le monde',
    },
  };

  String? get title {
    return _localizedValues[locale.languageCode]?['title'];
  }
}

/// A delegate class that loads the AppLocalizations class
class AppLocalizationsDelegate extends LocalizationsDelegate<AppLocalizations> {
  const AppLocalizationsDelegate();

  @override
  bool isSupported(Locale locale) => ['en', 'fr'].contains(locale.languageCode);

  @override
  Future<AppLocalizations> load(Locale locale) {
    return SynchronousFuture<AppLocalizations>(AppLocalizations(locale));
  }

  @override
  bool shouldReload(AppLocalizationsDelegate old) => false;
}
```

### Step 4: Generating localization files

Now, we need to generate the localization files for each language. Inside the `l10n` directory, create a new directory for each language you want to support. For example, create a `en` directory for English and a `fr` directory for French.

Inside each language directory, create a new file called `app_localizations.arb`. This file will contain the translated strings for the respective language. Here's an example of the contents of the `app_localizations.arb` file for English:

```dart
{
  "@@locale": "en",
  "title": "Hello World"
}
```

Similarly, create another `app_localizations.arb` file for French with the following contents:

```dart
{
  "@@locale": "fr",
  "title": "Bonjour le monde"
}
```

### Step 5: Loading and using localized strings

To load and use the localized strings in your Flutter application, open the `main.dart` file and modify it as follows:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';
import 'package:my_project/l10n/app_localizations.dart';

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
        const Locale('en'),
        const Locale('fr'),
      ],
      localeResolutionCallback: (locale, supportedLocales) {
        for (var supportedLocale in supportedLocales) {
          if (supportedLocale.languageCode == locale?.languageCode) {
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
    final loc = AppLocalizations.of(context);

    return Scaffold(
      appBar: AppBar(
        title: Text(loc?.title ?? ''),
      ),
      body: Center(
        child: Text(loc?.title ?? ''),
      ),
    );
  }
}
```

In this code, we have added the `AppLocalizationsDelegate` to the `localizationsDelegates` list and specified the supported locales. We have also added the localization logic to display the localized title in the app's `AppBar` and body.

### Step 6: Building and running the app

To build the app for the web, run the following command:

```dart
flutter build web
```

This will generate the necessary files for running the app on the web. To run the app, use the following command:

```dart
flutter run -d chrome
```

Now you can see your Flutter app running on Flutter WebGL with localization support!

### Conclusion

In this article, we explored how to implement localization in Flutter when targeting the web using Flutter WebGL. By following these steps, you can easily create multi-language applications that can be translated into different languages and cultures, providing a better user experience for your users.

#Flutter #WebGL #Localization
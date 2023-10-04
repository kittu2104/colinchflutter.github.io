---
layout: post
title: "Working with internationalization in Flutter using GetX"
description: " "
date: 2023-09-29
tags: [internationalization]
comments: true
share: true
---

In today's globalized world, it's important for mobile apps to support multiple languages and cultures. Flutter, being a popular cross-platform framework, has built-in support for internationalization (i18n). In this blog post, we'll explore how to leverage the GetX package in Flutter to easily implement internationalization in your app.

## What is GetX?

GetX is a powerful package for Flutter that provides a complete ecosystem bringing state management, dependency injection, and navigation solution in a simple and efficient way. With GetX, you can easily manage translations and handle internationalization within your app.

## Getting Started

To get started with internationalization using GetX, you need to follow these steps:

### Step 1: Install the dependencies

First, you need to add the GetX package to your `pubspec.yaml` file:

```dart
dependencies:
  flutter:
    sdk: flutter
  get: ^4.1.4
```

After updating the dependencies, run `flutter pub get` to install the GetX package.

### Step 2: Create localization files

Next, create `.json` files for each language you want to support. For example, create `en.json` for English and `es.json` for Spanish. The files should contain key-value pairs representing the translations.

`en.json`:
```json
{
  "title": "Welcome to my app!",
  "button_text": "Click me"
}
```

`es.json`:
```json
{
  "title": "¡Bienvenido a mi aplicación!",
  "button_text": "Haz clic aquí"
}
```

### Step 3: Implement the localization logic

In your Flutter project, create a new file called `app_translations.dart`. This file will contain the logic for loading the translations based on the device's locale:

```dart
import 'package:get/get.dart';

class AppTranslations extends Translations {
  @override
  Map<String, Map<String, String>> get keys => {
        'en': {
          'title': 'Welcome to my app!',
          'button_text': 'Click me',
        },
        'es': {
          'title': '¡Bienvenido a mi aplicación!',
          'button_text': 'Haz clic aquí',
        },
      };
}
```

### Step 4: Update your main.dart file

In your `main.dart` file, initialize GetX by using `GetMaterialApp` instead of `MaterialApp`:

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

import 'app_translations.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      translations: AppTranslations(),
      locale: Locale('en'), // Default locale
      fallbackLocale: Locale('en'),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'title'.tr,
              style: TextStyle(
                fontSize: 24,
                fontWeight: FontWeight.bold,
              ),
            ),
            SizedBox(height: 20),
            RaisedButton(
              onPressed: () {},
              child: Text('button_text'.tr),
            ),
          ],
        ),
      ),
    );
  }
}
```

### Step 5: Use translations in your app

Now you can use the translations in your app by simply calling `.tr` on the translation key. This allows GetX to fetch the appropriate translation based on the current locale.

## Conclusion

By following these steps, you can easily implement internationalization in your Flutter app using GetX. GetX provides a simple and efficient way to manage translations and make your app accessible to a global audience. So, go ahead and make your app multilingual using GetX!

#flutter #internationalization
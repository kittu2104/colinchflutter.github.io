---
layout: post
title: "Using GetX for real-time translation and language detection"
description: " "
date: 2023-09-29
tags: [GetX, translation]
comments: true
share: true
---

In today's globalized world, multilingual support has become an essential requirement for many applications. Whether you are building a website, a mobile app, or any other digital product, providing real-time translation and language detection is crucial for delivering a seamless user experience. In this blog post, we will explore how to achieve this using the **GetX** package, a powerful state management library for Flutter.

## What is GetX?

[GetX](https://pub.dev/packages/get) is a lightweight yet robust state management solution for Flutter that offers an array of features, including reactive programming, dependency injection, and much more. It simplifies the development process and enhances the performance of your application.

## Integrating Translation and Language Detection using GetX

To enable real-time translation and language detection in your Flutter application, follow these steps:

### Step 1: Add GetX Dependency

Add the `get` dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  get: ^4.3.8
```

### Step 2: Initialize GetX Localization

Create a new Dart file called `translation.dart` (or any preferred name) to handle localization and language detection. Import the necessary packages:

```dart
import 'package:get/get.dart';
import 'package:translator/translator.dart';
```

### Step 3: Create Localization Controller

Create a GetX controller class to manage the localization and language detection:

```dart
class LocalizationController extends GetxController {
  final translator = GoogleTranslator();

  var currentLocale = Locale('en').obs;
  var translatedText = ''.obs;
  var detectedLanguage = ''.obs;

  Future<void> translateText(String text, Locale locale) async {
    translatedText.value = await translator.translate(text, from: 'auto', to: locale.languageCode);
    currentLocale.value = locale;
  }

  Future<void> detectLanguage(String text) async {
    detectedLanguage.value = await translator.detect(text);
  }

  @override
  void onClose() {
    translator.close();
    super.onClose();
  }
}
```

This controller class uses the `translator` object from the `translator` package to perform translations and language detection. It maintains the current locale, translated text, and detected language as observable variables.

### Step 4: Implement Translation UI

Create a Flutter widget that allows users to enter text and select a target language:

```dart
class TranslationPage extends StatelessWidget {
  final LocalizationController controller = Get.put(LocalizationController());
  final TextEditingController textController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Translation'),
      ),
      body: Padding(
        padding: EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              controller: textController,
              decoration: InputDecoration(
                labelText: 'Enter Text',
              ),
            ),
            SizedBox(height: 16.0),
            ListTile(
              title: Text('Target Language:'),
              subtitle: DropdownButton<Locale>(
                value: controller.currentLocale.value,
                items: Languages.supportedLanguages
                    .map((locale) => DropdownMenuItem<Locale>(
                          value: locale,
                          child: Text(locale.languageCode),
                        ))
                    .toList(),
                onChanged: (Locale? value) {
                  if (value != null) {
                    controller.translateText(textController.text, value);
                  }
                },
              ),
            ),
            SizedBox(height: 16.0),
            Obx(() => Text('Detected Language: ${controller.detectedLanguage}')),
            SizedBox(height: 16.0),
            Obx(() => Text('Translated Text: ${controller.translatedText}')),
          ],
        ),
      ),
    );
  }
}
```

This widget utilizes the `LocalizationController` to perform translations and language detection. It provides a text field for users to enter text and a dropdown list to select the target language. The detected language and translated text are displayed on the screen using the `Obx` widget, which updates automatically when the underlying observable variables change.

### Step 5: Navigate to the Translation Page

Finally, navigate to the `TranslationPage` from your app's main file or any other desired location:

```dart
void main() {
  runApp(GetMaterialApp(
    home: TranslationPage(),
  ));
}
```

## Conclusion

Thanks to the power of **GetX**, integrating real-time translation and language detection into your Flutter application has never been easier. By following the steps outlined in this blog post, you can provide a seamless multilingual experience for your users. So go ahead, leverage **GetX** and take your application to a whole new level.

#flutter #GetX #translation
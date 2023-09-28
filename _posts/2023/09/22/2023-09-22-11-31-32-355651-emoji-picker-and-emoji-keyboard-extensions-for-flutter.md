---
layout: post
title: "Emoji picker and Emoji keyboard extensions for Flutter"
description: " "
date: 2023-09-22
tags: [emoji]
comments: true
share: true
---

Emojis have become an integral part of our digital communication. They add an extra level of expressiveness and fun to our messages, social media posts, and even app interfaces. As a Flutter developer, you may want to integrate emojis seamlessly into your app to enhance user engagement and make the user experience more enjoyable. In this blog post, we will explore two popular options for adding emoji picker and emoji keyboard extensions to your Flutter app.

## 1. Emoji Picker

An emoji picker allows users to conveniently select emojis from a wide range of options. One popular package for implementing an emoji picker in your Flutter app is the `flutter_emoji_picker` package. It provides a simple and customizable emoji picker widget that you can integrate into your app.

To use `flutter_emoji_picker`, you need to add it as a dependency in your app's `pubspec.yaml` file:

```yaml
dependencies:
  flutter_emoji_picker: ^version_number
```

Here's an example of how to use the emoji picker in your code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_emoji_picker/flutter_emoji_picker.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text("Emoji Picker Example"),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () async {
              final selectedEmoji = await EmojiPicker.showPicker(context);
              if (selectedEmoji != null) {
                print("Selected Emoji: $selectedEmoji");
              }
            },
            child: Text("Open Emoji Picker"),
          ),
        ),
      ),
    );
  }
}
```

In the above example, we created a simple Flutter app with an `ElevatedButton` widget. When the button is pressed, the emoji picker is displayed using the `showPicker` method from the `EmojiPicker` class. The selected emoji is printed to the console.

With `flutter_emoji_picker`, you can customize the appearance of the emoji picker widget to match your app's design and style. You can modify the number of rows, specify the number of emojis per row, and even filter specific categories of emojis.

## 2. Emoji Keyboard Extensions

If you want to take emoji integration a step further, you can consider implementing an emoji keyboard extension. This feature allows users to access emojis directly from the keyboard while typing, without the need to switch between keyboards or emoji picker interfaces. One popular package for implementing emoji keyboard extensions in Flutter is the `flutter_emoji_keyboard` package.

To use `flutter_emoji_keyboard`, add it as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_emoji_keyboard: ^version_number
```

Here's an example of how to use the emoji keyboard extension:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_emoji_keyboard/flutter_emoji_keyboard.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: EmojiKeyboard(
        child: Scaffold(
          appBar: AppBar(
            title: Text("Emoji Keyboard Extension Example"),
          ),
          body: EmojiEditableText(
            hintText: 'Type a message...',
          ),
        ),
      ),
    );
  }
}
```

In this example, we wrapped our app with the `EmojiKeyboard` widget which provides the emoji keyboard extension functionality. Inside the `EmojiKeyboard`, we have a `Scaffold` with an `EmojiEditableText` widget. The `EmojiEditableText` widget is responsible for displaying the editable text field with emoji support.

By integrating the `flutter_emoji_keyboard` package into your Flutter app, you can allow your users to easily insert emojis while typing, improving their messaging experience.

## Conclusion

Adding emoji picker and emoji keyboard extensions to your Flutter app can greatly enhance the user experience and bring an element of fun to your application. We explored two popular packages, `flutter_emoji_picker` and `flutter_emoji_keyboard`, which provide easy-to-use solutions for integrating emojis into your app. With these packages, you can allow your users to select emojis from a picker interface or access emojis directly from the keyboard. Experiment with these packages and make your app messaging more expressive and engaging.

#flutter #emoji #Keyboard
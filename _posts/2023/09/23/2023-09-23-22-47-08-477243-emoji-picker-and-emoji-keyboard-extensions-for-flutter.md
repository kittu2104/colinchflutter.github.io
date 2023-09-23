---
layout: post
title: "Emoji picker and Emoji keyboard extensions for Flutter"
description: " "
date: 2023-09-23
tags: [flutter, emoji]
comments: true
share: true
---

Are you looking to add a fun and engaging feature to your Flutter app? Look no further than emoji picker and emoji keyboard extensions! Emoji pickers allow users to easily select and insert emojis into text fields, while emoji keyboards provide a dedicated keyboard for users to quickly access and insert emojis. In this blog post, we will explore how to integrate emoji picker and emoji keyboard extensions into your Flutter app.

## What are Emoji Picker and Emoji Keyboard Extensions?

Emoji picker and emoji keyboard extensions are tools that enhance the user experience by making it easier to add emojis to text fields. With an emoji picker, users can choose from a wide range of emojis available in a popup window or a separate screen. An emoji keyboard, on the other hand, replaces the standard keyboard with a dedicated keyboard that consists only of emojis.

## Adding Emoji Picker to your Flutter app

To add an emoji picker to your Flutter app, you can use the `emoji_picker` package available on pub.dev. Start by adding it to your `pubspec.yaml` file:

```dart
dependencies:
  emoji_picker: ^0.1.2
```

Once you have added the package, you can import it into your Flutter file:

```dart
import 'package:emoji_picker/emoji_picker.dart';
```

Next, you can use the `EmojiPicker` widget in your app's UI:

```dart
EmojiPicker(
  onEmojiSelected: (emoji) {
    // handle selected emoji
  },
);
```

The `onEmojiSelected` callback allows you to handle the selected emoji and insert it into the desired text field.

## Adding Emoji Keyboard Extension to your Flutter app

To add an emoji keyboard extension to your Flutter app, you can use the `flutter_emoji_keyboard` package available on pub.dev. Begin by adding it to your `pubspec.yaml` file:

```dart
dependencies:
  flutter_emoji_keyboard: ^0.1.0
```

After adding the package, import it into your Flutter file:

```dart
import 'package:flutter_emoji_keyboard/flutter_emoji_keyboard.dart';
```

Now, you can use the `EmojiKeyboard` widget in your app's UI:

```dart
TextField(
  keyboardType: EmojiKeyboard.inputType,
);
```

Assigning `EmojiKeyboard.inputType` to the `keyboardType` property of the `TextField` replaces the standard keyboard with the emoji keyboard, allowing users to easily access and insert emojis.

## Conclusion

Emoji picker and emoji keyboard extensions are valuable additions to any Flutter app, making it effortless for users to express themselves through emojis. By incorporating these features, you can enhance the user experience and make your app more engaging. Whether it's a standalone emoji picker or a dedicated emoji keyboard, Flutter provides the flexibility and ease of integration necessary to implement these extensions seamlessly.

#flutter #emoji
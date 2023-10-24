---
layout: post
title: "Cupertino text style in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [References]
comments: true
share: true
---

When building Flutter applications, you have the option to use either `MaterialApp` or `CupertinoApp` as the root widget. These two widgets provide different design languages - Material Design for `MaterialApp` and Cupertino Design for `CupertinoApp`. One noticeable difference between the two is how text styles are handled.

## MaterialApp Text Style

When using `MaterialApp`, the default text style follows the guidelines of Material Design. This means that the text is typically displayed using the Roboto font on Android and the San Francisco font on iOS. The text style properties, such as font family, font size, and font weight, can be customized using the `TextStyle` class. You can pass a `TextStyle` object to various widgets, such as `Text`, `TextField`, and `RichText`, to define the appearance of the text.

Example code:

```dart
TextStyle myTextStyle = TextStyle(
  fontSize: 16,
  fontWeight: FontWeight.bold,
);

Text(
  'Hello, World!',
  style: myTextStyle,
)
```

## CupertinoApp Text Style

In contrast, when using `CupertinoApp`, the default text style follows the guidelines of Cupertino Design. This means that the text is displayed using the San Francisco font on both Android and iOS. Similar to `MaterialApp`, you can customize the text style using the `TextStyle` class. However, the recommended text style properties, such as font size and weight, may be different from the Material Design guidelines.

Example code:

```dart
TextStyle myTextStyle = TextStyle(
  fontSize: 18,
  fontWeight: FontWeight.w500,
);

Text(
  'Hello, World!',
  style: myTextStyle,
)
```

It's worth noting that while the default text styles differ between `MaterialApp` and `CupertinoApp`, you can still override them to achieve a consistent look across platforms. Additionally, Flutter provides a `DefaultTextStyle` widget that wraps its descendants and sets the default text style for the subtree.

By understanding the differences in text styles between `MaterialApp` and `CupertinoApp`, you can choose the appropriate widget for your application based on the desired design language. Remember to consider the platform-specific guidelines and ensure a cohesive user experience.

#References
1. [Flutter Documentation - Text Widget](https://api.flutter.dev/flutter/widgets/Text-class.html)
2. [Flutter Documentation - TextStyle Class](https://api.flutter.dev/flutter/painting/TextStyle-class.html)
3. [Material Design Typography Guidelines](https://material.io/design/typography/overview.html)
4. [Cupertino Design Guidelines](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/typography/)
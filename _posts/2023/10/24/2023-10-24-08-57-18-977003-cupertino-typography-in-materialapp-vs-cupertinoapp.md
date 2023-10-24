---
layout: post
title: "Cupertino typography in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing a Flutter application, you have the choice between using the `MaterialApp` or `CupertinoApp` widget from the Flutter framework. Each widget provides a different style and user interface based on different design guidelines.

One key aspect where these widgets differ is the typography. In this blog post, we will explore the differences in typography between `MaterialApp` and `CupertinoApp`.

## Material Design Typography in MaterialApp

If you choose to use the `MaterialApp` widget, you'll get the default typography based on the Material Design guidelines. Material Design focuses on providing a clean and minimalist UI with readable and consistent typography.

The Material Design typography system consists of various text styles such as headline, subtitle, body text, and more. These text styles are defined by default and can be easily customized to meet your specific needs.

To use Material Design typography, you can simply use the predefined text styles provided by Flutter, such as `TextStyle.headline`, `TextStyle.bodyText1`, or `TextStyle.caption`.

Here's an example of using Material Design typography in a `MaterialApp`:

```dart
Text(
  'Hello, World!',
  style: TextStyle(
    fontSize: 24,
    fontWeight: FontWeight.bold,
    fontStyle: FontStyle.italic,
  ),
);
```

In the above code snippet, we specified the font size, weight, and style for the text. These properties can be adjusted as per the Material Design guidelines.

## Cupertino Typography in CupertinoApp

On the other hand, if you opt for the `CupertinoApp` widget, you'll follow the Cupertino Design guidelines, which are used in iOS applications. The typography in Cupertino design is distinct and has a more skeuomorphic and textured appearance.

Cupertino typography also includes various text styles such as largeTitle, title, body, caption, etc. To use Cupertino typography in your `CupertinoApp`, you can use the predefined text styles provided by Flutter, such as `CupertinoTheme.of(context).textTheme.textStyle`.

Here's an example of using Cupertino typography in a `CupertinoApp`:

```dart
Text(
  'Hello, World!',
  style: CupertinoTheme.of(context).textTheme.textStyle.copyWith(
    fontSize: 24,
    fontWeight: FontWeight.bold,
    fontStyle: FontStyle.italic,
  ),
);
```

In the above code snippet, we utilized the `CupertinoTheme` to access the Cupertino typography styles and then applied the desired text style to the `Text` widget.

## Conclusion

When choosing between `MaterialApp` and `CupertinoApp`, it's essential to consider the design guidelines you want to follow and the platform-specific look and feel you want to achieve.

By using `MaterialApp`, you get the sleek and modern typography provided by Material Design. On the other hand, `CupertinoApp` offers skeuomorphic and textured typography aligned with iOS design principles.

By understanding these typography differences, you can create visually appealing Flutter applications following the design guidelines of your target platform.

[Official Material Design Documentation](https://material.io/design/typography/overview.html)
[Official Cupertino Design Documentation](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/typography/)
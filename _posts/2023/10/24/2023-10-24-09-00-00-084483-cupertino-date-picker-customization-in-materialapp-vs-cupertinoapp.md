---
layout: post
title: "Cupertino date picker customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [Cupertino]
comments: true
share: true
---

In Flutter, you can choose between two different sets of UI components: Material Design and Cupertino Design. The Cupertino design language is specifically tailored for iOS apps, while Material Design is a more generalized design language that can be used across different platforms.

When it comes to customizing the Cupertino date picker, you'll need to consider the differences between using the `MaterialApp` and `CupertinoApp` widgets in your Flutter app.

## MaterialApp

The `MaterialApp` widget is used to create apps with Material Design. If you are using this widget and want to customize the Cupertino date picker, you'll need to wrap it with a `Theme` widget and set the `platform` property to `TargetPlatform.iOS`.

Here's an example of how to customize the Cupertino date picker in a `MaterialApp`:

```dart
return MaterialApp(
  theme: ThemeData(
    platform: TargetPlatform.iOS,
  ),
  home: Scaffold(
    appBar: AppBar(
      title: Text('My App'),
    ),
    body: Center(
      child: CupertinoDatePicker(
        // Customize the date picker here
      ),
    ),
  ),
);
```

## CupertinoApp

On the other hand, the `CupertinoApp` widget is used to create apps with Cupertino Design. Since the Cupertino date picker is already designed using Cupertino components, you don't need to customize it further when using `CupertinoApp`.

Here's an example of how to use the Cupertino date picker in a `CupertinoApp`:

```dart
return CupertinoApp(
  home: CupertinoPageScaffold(
    navigationBar: CupertinoNavigationBar(
      middle: Text('My App'),
    ),
    child: Center(
      child: CupertinoDatePicker(
        // Customize the date picker here
      ),
    ),
  ),
);
```

## Conclusion

In summary, when it comes to customizing the Cupertino date picker in your Flutter app, the approach differs depending on whether you are using the `MaterialApp` or `CupertinoApp`. With `MaterialApp`, you need to wrap it with a `Theme` widget and set the `platform` property to `TargetPlatform.iOS`. On the other hand, with `CupertinoApp`, you can directly use the Cupertino date picker without further customization.

# References
- Flutter Documentation: [https://flutter.dev/docs](https://flutter.dev/docs)
- Material Design Guidelines: [https://material.io/design](https://material.io/design)
- Cupertino Design Guidelines: [https://developer.apple.com/design/human-interface-guidelines/ios/overview/themes/](https://developer.apple.com/design/human-interface-guidelines/ios/overview/themes/)

#Flutter #Cupertino
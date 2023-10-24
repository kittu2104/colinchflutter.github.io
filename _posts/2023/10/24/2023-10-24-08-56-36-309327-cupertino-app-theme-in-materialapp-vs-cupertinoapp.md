---
layout: post
title: "Cupertino app theme in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing a mobile app using Flutter, you have the option to choose between two different app themes: `MaterialApp` and `CupertinoApp`. Both provide a set of widgets and styles that give your app a polished and consistent look. 

## MaterialApp

`MaterialApp` is the default app theme in Flutter and follows the Material Design guidelines. This means that your app will have a modern, visually appealing look with layers, shadows, and intuitive navigation patterns. 

To use `MaterialApp` as your app theme, simply add it as the root widget in your Flutter app. It provides various properties, such as `title`, `theme`, and `home`, where you can customize the app's appearance and behavior.

```dart
void main() {
  runApp(MaterialApp(
    title: 'My App',
    theme: ThemeData(
      primarySwatch: Colors.blue,
      accentColor: Colors.orange,
    ),
    home: MyHomePage(),
  ));
}
```

## CupertinoApp

On the other hand, `CupertinoApp` follows the design principles of Apple's iOS. If you want your app to have an iOS-like look and feel, you can choose `CupertinoApp` as your app theme. 

Similar to `MaterialApp`, you can customize the appearance and behavior of the app using properties like `title`, `theme`, and `home`. The main difference is that `CupertinoApp` provides a set of iOS-specific widgets and styles.

```dart
void main() {
  runApp(CupertinoApp(
    title: 'My App',
    theme: CupertinoThemeData(
      primaryColor: Colors.blue,
      scaffoldBackgroundColor: Colors.white,
    ),
    home: MyHomePage(),
  ));
}
```

## Choosing the Right Theme

The choice between `MaterialApp` and `CupertinoApp` depends on the platform you are targeting and the aesthetic you want to achieve.

- If you are developing a cross-platform app or targeting Android devices, using `MaterialApp` is recommended. It provides a consistent experience across different devices and follows Google's Material Design guidelines.

- If you are specifically targeting iOS devices or want to achieve an iOS-like look, you can choose `CupertinoApp`. This will give your app an authentic iOS appearance and make it feel native on Apple devices.

Remember to import the necessary packages (`material` and `cupertino`) before using `MaterialApp` or `CupertinoApp` in your code.

Overall, both themes offer beautiful designs and numerous customization options to create stunning mobile apps.
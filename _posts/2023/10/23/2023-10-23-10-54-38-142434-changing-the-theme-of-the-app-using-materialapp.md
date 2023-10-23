---
layout: post
title: "Changing the theme of the app using MaterialApp."
description: " "
date: 2023-10-23
tags: [Reference]
comments: true
share: true
---

When developing a mobile app using Flutter, it is common to want to customize its appearance and give it a unique and visually appealing look. Flutter provides a powerful widget called `MaterialApp` that allows you to easily change the theme of your app.

The theme of an app defines the overall colors, font styles, and other visual properties. By using `MaterialApp`, you can define a custom theme and apply it to your entire app with just a few lines of code.

To change the theme of your app using `MaterialApp`, follow the steps below:

## Step 1: Declare a custom theme

First, you need to declare a custom theme for your app. You can do this by creating a `ThemeData` object and setting its properties according to your desired theme.

```dart
final CustomThemeData = ThemeData(
  primaryColor: Colors.blue,
  accentColor: Colors.orange,
  fontFamily: 'Roboto',
  // Add more properties to customize your theme
);
```

In the above example, we have defined a custom theme with a blue primary color, an orange accent color, and the 'Roboto' font family.

## Step 2: Apply the custom theme using MaterialApp

Next, you need to apply the custom theme to your app by wrapping your entire app's widget tree with the `MaterialApp` widget and passing the `theme` parameter with your custom theme.

```dart
void main() {
  runApp(
    MaterialApp(
      theme: CustomThemeData,
      home: MyApp(),
    ),
  );
}
```

In this example, the `theme` parameter of `MaterialApp` is set to the previously declared `CustomThemeData`.

## Step 3: Utilize the custom theme

Once you have applied the custom theme to your app using `MaterialApp`, you can start utilizing it in different widgets throughout your app.

For example, you can set the background color of a `Container` widget to the primary color of your theme like this:

```dart
Container(
  color: Theme.of(context).primaryColor,
  // Other widget properties
)
```

In the above code snippet, `Theme.of(context)` returns the current app's theme, and `.primaryColor` accesses the primary color property defined in the custom theme.

By utilizing the custom theme, you can easily maintain consistency in the visual style of your app and change the overall look and feel with just a few modifications to the theme properties.

To conclude, with the help of `MaterialApp` and a custom theme, you can change the theme of your app in Flutter effortlessly. This allows you to have more control over the visual aspects of your app and create a cohesive user experience.

#Reference
- [MaterialApp class - Flutter API Documentation](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
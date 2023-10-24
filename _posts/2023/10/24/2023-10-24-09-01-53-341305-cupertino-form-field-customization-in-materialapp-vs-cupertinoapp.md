---
layout: post
title: "Cupertino form field customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [References]
comments: true
share: true
---

When it comes to customizing form fields in Flutter, you have two options: using the `MaterialApp` or the `CupertinoApp`. Both widgets provide the necessary components to create forms with various fields, but there are some differences in terms of styling and design. Let's explore how Cupertino form fields can be customized in each of these apps.

## Cupertino Form Fields in MaterialApp

In a `MaterialApp`, you can use the `TextFormField` widget to create form fields. This widget is part of the Material Design language and is styled accordingly. To customize the appearance of the `TextFormField`, you can use the `decoration` property to define the border, background color, and other visual elements.

Here's an example of a customized `TextFormField` in a `MaterialApp`:

```dart
TextFormField(
  decoration: InputDecoration(
    border: OutlineInputBorder(
      borderRadius: BorderRadius.circular(10.0),
    ),
    filled: true,
    fillColor: Colors.grey[200],
    hintText: 'Enter your name',
    labelText: 'Name',
    prefixIcon: Icon(Icons.person),
  ),
)
```

In this snippet, we are defining a rounded border, grey background color, placeholder text, label, and a prefix icon for the form field.

## Cupertino Form Fields in CupertinoApp

On the other hand, the `CupertinoApp` provides form field widgets specifically designed for iOS-like interfaces. The main widget for creating form fields in this context is `CupertinoTextField`. This widget follows the iOS design guidelines and provides customization options tailored to Cupertino styling.

To customize the `CupertinoTextField`, you can use properties such as `decoration`, `placeholder`, `prefix`, `suffix`, and others. These properties allow you to define various visual elements like borders, placeholder text, icons, and more.

Here's an example of a customized `CupertinoTextField` in a `CupertinoApp`:

```dart
CupertinoTextField(
  decoration: BoxDecoration(
    border: Border.all(color: CupertinoColors.systemGrey),
    borderRadius: BorderRadius.circular(10.0),
    color: CupertinoColors.lightBackgroundGray,
  ),
  placeholder: 'Enter your name',
  prefix: Icon(
    CupertinoIcons.person,
    color: CupertinoColors.systemGrey,
    size: 20.0,
  ),
)
```

In this code snippet, we are defining a border with the system grey color, light gray background color, placeholder text, and a prefix icon using the Cupertino icons.

## Summary

In summary, if you are building a Flutter app with a Material Design theme, using the `TextFormField` widget in a `MaterialApp` allows you to customize form fields using Material Design styling. On the other hand, if you are targeting an iOS-like interface with the `CupertinoApp`, the `CupertinoTextField` widget provides customization options tailored to Cupertino styling.

Remember that both widget options can be used in either `MaterialApp` or `CupertinoApp` based on your app's design requirements and target platform.

#References
- Flutter Documentation: [TextFormField](https://api.flutter.dev/flutter/material/TextFormField-class.html)
- Flutter Cupertino Widgets: [CupertinoTextField](https://api.flutter.dev/flutter/cupertino/CupertinoTextField-class.html)
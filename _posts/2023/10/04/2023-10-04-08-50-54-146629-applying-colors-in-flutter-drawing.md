---
layout: post
title: "Applying colors in Flutter drawing"
description: " "
date: 2023-10-04
tags: [built, custom]
comments: true
share: true
---

In Flutter, colors play a vital role in the UI design of your app. You can apply different colors to various UI elements such as text, buttons, background, and more. In this blog post, we'll explore different ways to apply colors in Flutter drawing.

## Table of Contents
- [Built-in Colors](#built-in-colors)
- [Custom Colors](#custom-colors)
- [Applying Colors](#applying-colors)
- [Conclusion](#conclusion)

## Built-in Colors

Flutter provides a set of built-in colors that you can directly use in your app. These colors are available as static constants in the `Colors` class. Let's take a look at some commonly used built-in colors:

```dart
import 'package:flutter/material.dart';

Color primaryColor = Colors.blue; 
Color secondaryColor = Colors.red;
Color accentColor = Colors.yellow;
Color textColor = Colors.black;
Color backgroundColor = Colors.white;
```

These are just a few examples, but Flutter provides many more built-in colors that you can use in your app.

## Custom Colors

Besides the built-in colors, you can also create custom colors in Flutter by specifying their RGB values. You can use the `Color` class constructor to create custom colors. Here's an example:

```dart
import 'package:flutter/material.dart';

Color customColor = Color(0xFFAABBCC);
```

In the above example, `0xFF` represents the alpha value, and `AABBCC` represents the RGB values. Replace `AABBCC` with the desired RGB values to create your custom color.

## Applying Colors

You can apply colors to different UI elements in Flutter in multiple ways. Let's explore some common scenarios:

### Text Color

To apply a specific color to a text widget, you can use the `style` property of the `Text` widget and specify the desired color:

```dart
Text(
  'Hello, Flutter!',
  style: TextStyle(color: textColor),
),
```

### Background Color

To set the background color of a container, you can use the `color` property:

```dart
Container(
  color: backgroundColor,
  child: Text('This is a container with a background color.'),
),
```

### Button Color

To customize the color of a button widget, you can use the `color` property:

```dart
ElevatedButton(
  onPressed: () {},
  style: ButtonStyle(
    backgroundColor: MaterialStateProperty.all(primaryColor),
  ),
  child: Text('Click me'),
),
```

## Conclusion

Colors are an essential part of Flutter app development. In this blog post, we explored how to use both built-in and custom colors in your app. We also looked at different ways to apply colors to text, containers, and buttons in Flutter.

By effectively utilizing colors, you can enhance the visual appeal and user experience of your Flutter app. So go ahead and start implementing colorful designs in your next Flutter project!

#flutter #colors
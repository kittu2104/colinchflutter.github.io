---
layout: post
title: "Cupertino text field customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [References]
comments: true
share: true
---

When working with Flutter, you have two options for customizing the appearance of text fields using Cupertino styling: within a `MaterialApp` or a `CupertinoApp`. Both approaches offer a similar set of customization, but there are some differences in terms of appearance and behavior. In this blog post, we will explore how to customize Cupertino text fields in both `MaterialApp` and `CupertinoApp`.

## Setting up MaterialApp

To get started with customizing Cupertino text fields in a `MaterialApp`, make sure to add the following dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
```

Then, import the necessary packages in your Dart code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';
```

Next, set up your `MaterialApp` and create a Cupertino text field:

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Cupertino TextField Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: CupertinoTextField(
        placeholder: 'Enter your text',
      ),
    );
  }
}
```

With this setup, you will have a basic Cupertino-styled text field in your `MaterialApp` environment.

## Customizing the MaterialApp Cupertino TextField

To customize the appearance and behavior of the Cupertino text field in a `MaterialApp`, you can provide additional properties to the `CupertinoTextField` widget. Here are a few examples:

### Placeholder Text Color

To change the color of the placeholder text, use the `placeholderStyle` property:

```dart
CupertinoTextField(
  placeholder: 'Enter your text',
  placeholderStyle: TextStyle(
    color: Colors.red,
  ),
),
```

### Text Input Decoration

To provide an outline or underline style for the text field, use the `decoration` property:

```dart
CupertinoTextField(
  placeholder: 'Enter your text',
  decoration: BoxDecoration(
    border: Border.all(color: Colors.grey),
    borderRadius: BorderRadius.circular(10.0),
  ),
),
```

### Text Alignment

To specify the alignment of the text within the text field, use the `textAlign` property:

```dart
CupertinoTextField(
  placeholder: 'Enter your text',
  textAlign: TextAlign.center,
),
```

## Setting up CupertinoApp

To customize Cupertino text fields using a `CupertinoApp`, make sure to import the necessary packages:

```dart
import 'package:flutter/cupertino.dart';
```

Next, set up your `CupertinoApp` and create a Cupertino text field:

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      title: 'Cupertino TextField Demo',
      home: CupertinoTextField(
        placeholder: 'Enter your text',
      ),
    );
  }
}
```

With this setup, you will have a basic Cupertino-styled text field in your `CupertinoApp` environment.

## Customizing the CupertinoApp Cupertino TextField

To customize the appearance and behavior of the Cupertino text field in a `CupertinoApp`, you can provide additional properties to the `CupertinoTextField` widget. Here are a few examples:

### Placeholder Text Color

To change the color of the placeholder text, use the `placeholderStyle` property:

```dart
CupertinoTextField(
  placeholder: 'Enter your text',
  placeholderStyle: TextStyle(
    color: CupertinoColors.systemRed,
  ),
),
```

### Text Input Decoration

To provide an outline or underline style for the text field, use the `decoration` property:

```dart
CupertinoTextField(
  placeholder: 'Enter your text',
  decoration: BoxDecoration(
    border: Border.all(color: CupertinoColors.systemGrey),
    borderRadius: BorderRadius.circular(10.0),
  ),
),
```

### Text Alignment

To specify the alignment of the text within the text field, use the `textAlign` property:

```dart
CupertinoTextField(
  placeholder: 'Enter your text',
  textAlign: TextAlign.center,
),
```

## Conclusion

Both `MaterialApp` and `CupertinoApp` can be used to customize Cupertino text fields in your Flutter application. While `MaterialApp` provides a more Material Design-focused styling, `CupertinoApp` offers a native iOS look and feel. Choose the approach that aligns best with your app's overall design and branding.

By utilizing the customization properties provided by Flutter's Cupertino text field widget, you can create visually appealing and functional text fields for your iOS-style applications.

#References

To learn more about Cupertino Text Fields and their customization options, consult the official Flutter documentation:

1. [CupertinoTextField class - Flutter API documentation](https://api.flutter.dev/flutter/cupertino/CupertinoTextField-class.html)
2. [CupertinoApp class - Flutter API documentation](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
---
layout: post
title: "CupertinoTimePicker widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When working with Flutter, you have the flexibility to choose different types of widgets for your app's UI. Two popular options are the `MaterialApp` and `CupertinoApp` widgets. These widgets come with their own set of UI components, such as the `CupertinoTimePicker`, which can be used to select a specific time.

## CupertinoTimePicker in MaterialApp

To use the `CupertinoTimePicker` widget in a `MaterialApp`, you first need to import the `cupertino` package:

```dart
import 'package:flutter/cupertino.dart';
```

Then, you can use the `CupertinoTimePicker` widget like this:

```dart
CupertinoTimePicker(
  mode: CupertinoDatePickerMode.time,
  onDateTimeChanged: (DateTime newTime) {
    // Handle the selected time
  },
);
```

In a `MaterialApp`, the `CupertinoTimePicker` widget will be rendered using the Material Design style. It will have a different look and feel compared to when it is used within a `CupertinoApp`.

## CupertinoTimePicker in CupertinoApp

To use the `CupertinoTimePicker` widget in a `CupertinoApp`, you don't need to import any additional packages. The `CupertinoApp` already includes the Cupertino widgets by default.

Here's an example of using the `CupertinoTimePicker` widget in a `CupertinoApp`:

```dart
CupertinoDatePicker(
  mode: CupertinoDatePickerMode.time,
  onDateTimeChanged: (DateTime newTime) {
    // Handle the selected time
  },
);
```

In a `CupertinoApp`, the `CupertinoTimePicker` widget will be rendered using the Cupertino style, giving it the native iOS look and feel.

## Conclusion

Both the `MaterialApp` and `CupertinoApp` widgets are great choices for building Flutter apps. The choice between using `CupertinoTimePicker` in a `MaterialApp` or `CupertinoApp` depends on the overall design and style you want to achieve in your app's UI.

Remember to import the necessary packages and choose the appropriate widget based on the desired visual style.

#flutter #cupertino
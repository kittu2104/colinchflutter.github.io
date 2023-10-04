---
layout: post
title: "How to listen for high contrast mode changes using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [accessibility]
comments: true
share: true
---

In some cases, you may want your Flutter application to be aware of changes in the high contrast mode of the device it is running on. High contrast mode enhances the visibility of UI elements for users with visual impairments. Flutter provides a MediaQuery class that allows you to listen for these changes and update your UI accordingly.

To listen for high contrast mode changes, follow these steps:

1. Import the `flutter/services.dart` package in your Flutter project.

```dart
import 'package:flutter/services.dart';
```

2. Create a `MediaQueryData` object to retrieve information about the current media and high contrast mode.

```dart
MediaQueryData _mediaQueryData = MediaQueryData();
```

3. Subscribe to changes in the high contrast mode using the `setAccessibilityFeaturesChangedCallback` method.

```dart
void _listenForHighContrastModeChanges() {
  SystemChannels.accessibility.setAccessibilityFeaturesChangedCallback(() {
    setState(() {
      _mediaQueryData = MediaQueryData.fromWindow(WidgetsBinding.instance!.window);
    });
  });
}
```

4. Use the `highContrast` property of the `MediaQueryData` object to determine the current high contrast mode.

```dart
bool isHighContrastMode = _mediaQueryData.highContrast;
```

5. Optionally, you can update your UI based on the high contrast mode value. For example, you can change the color scheme or adjust the contrast of your UI elements.

```dart
ColorScheme colorScheme = isHighContrastMode ? ColorScheme.highContrastDark() : ColorScheme.light();
```

Remember to call the `_listenForHighContrastModeChanges` method when your widget initializes or when you want to start listening for high contrast mode changes.

Now, your Flutter application will be responsive to changes in the high contrast mode of the device it is running on. You can use this feature to make your app more accessible for users with visual impairments.

#flutter #accessibility
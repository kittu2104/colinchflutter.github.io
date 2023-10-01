---
layout: post
title: "How to get the system UI mode using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

When building a Flutter app, it is important to be aware of the system UI mode, which refers to the current state of the device's status bar and navigation bar. For instance, in dark mode, the UI elements may have a dark background color, while in light mode, the background color could be light.

To retrieve the system UI mode in Flutter, we can use the `MediaQuery` class. The `MediaQuery` class provides information about the current app context, including the system UI settings.

To get the system UI mode, you can follow these steps:

1. Import the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
```

2. Use the `MediaQuery` class to retrieve the brightness value of the system UI:

```dart
Brightness getSystemUIBrightness() {
  var brightness = MediaQuery.of(context).platformBrightness;
  
  if (brightness == Brightness.dark) {
    return Brightness.dark;
  } else {
    return Brightness.light;
  }
}
```

3. Call the `getSystemUIBrightness` function to get the current system UI brightness:

```dart
var brightness = getSystemUIBrightness();
print('System UI brightness: $brightness');
```

By calling the `getSystemUIBrightness` function, you will be able to receive the current system UI brightness. The `platformBrightness` property returns a `Brightness` enum value, which can be either `Brightness.dark` or `Brightness.light`.

Now, you can use the system UI mode information to customize your Flutter app's theme or adapt the UI elements accordingly.

# Conclusion

Understanding the system UI mode can help you create more engaging and user-friendly Flutter apps. By using the `MediaQuery` class in Flutter, you can easily retrieve the system UI mode and adapt your app's UI elements accordingly.
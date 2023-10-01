---
layout: post
title: "How to get device insets using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [flutter, dart]
comments: true
share: true
---
title: Getting Device Insets with MediaQuery in Flutter
description: Learn how to retrieve device insets using the MediaQuery class in Flutter for better screen handling.
---

In Flutter, when building user interfaces, it's important to handle different screen sizes and device insets properly. Device insets refer to the areas on the screen that are reserved for things like system status bars, notches, or rounded corners.

To retrieve the device insets in Flutter, we can use the `MediaQuery` class which provides information about the current screen and device. Below is an example of how to get device insets using `MediaQuery` in Flutter:

```dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final EdgeInsets deviceInsets = MediaQuery.of(context).padding;
    // ...
    return Container(
      // Use the obtained deviceInsets to handle screen content accordingly
    );
  }
}
```

In the above code, we first import the `flutter/material.dart` package. Then, inside the `build` method of our app, we retrieve the device insets using `MediaQuery.of(context).padding`. The `padding` property of the `MediaQuery` class returns the insets in the form of an `EdgeInsets` object.

Once we have obtained the device insets, we can use them to handle our screen content accordingly. For example, we can adjust the positioning or size of certain widgets to avoid being obstructed by device insets.

By using `MediaQuery` to get device insets, our app will be able to adapt to different screen sizes and configurations, providing a better user experience on a wide range of devices.

#flutter #dart
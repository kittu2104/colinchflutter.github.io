---
layout: post
title: "MediaQuery highContrastChanged in Flutter"
description: " "
date: 2023-10-01
tags: [accessibility]
comments: true
share: true
---

In Flutter, the `MediaQuery.highContrastChanged` property is used to detect changes in the high contrast mode of the device. The high contrast mode is a system setting that adjusts the appearance of the user interface to increase visibility for users with visual impairments.

When the high contrast mode is enabled or disabled, the `highContrastChanged` property can be used to trigger updates in the UI to adapt to the new visual settings. This is especially important for applications that need to provide an accessible experience for all users.

To use the `highContrastChanged` property, you first need to get the `MediaQueryData` object, which provides information about the device's screen and system configuration. You can access it using the `MediaQuery.of(context)` method.

Here's an example of how you can listen to changes in the high contrast mode using a `MediaQuery` widget:

```dart
import 'package:flutter/material.dart';

class HighContrastDetectionWidget extends StatefulWidget {
  @override
  _HighContrastDetectionWidgetState createState() =>
      _HighContrastDetectionWidgetState();
}

class _HighContrastDetectionWidgetState
    extends State<HighContrastDetectionWidget> {
  bool _isHighContrastEnabled = false;

  @override
  Widget build(BuildContext context) {
    return MediaQuery(
      data: MediaQuery.of(context).copyWith(),
      child: Builder(
        builder: (BuildContext context) {
          final bool isHighContrast =
              MediaQuery.of(context).highContrastChanged;

          if (_isHighContrastEnabled != isHighContrast) {
            setState(() {
              // Update UI based on high contrast mode change
              _isHighContrastEnabled = isHighContrast;
            });
          }

          return Text(
            'High contrast mode: ${_isHighContrastEnabled ? 'Enabled' : 'Disabled'}',
            style: TextStyle(
              color: _isHighContrastEnabled ? Colors.black : Colors.white,
              fontWeight: FontWeight.bold,
            ),
          );
        },
      ),
    );
  }
}
```

In this example, we create a stateful widget `HighContrastDetectionWidget` that listens to changes in the high contrast mode. Inside the `build` method, we wrap our UI with a `MediaQuery` widget to get access to the `highContrastChanged` property. We then compare the current value of `_isHighContrastEnabled` with the value obtained from `highContrastChanged` and update the UI accordingly.

Please note that the `highContrastChanged` property is only available on platforms that support high contrast mode. It may not work on all devices or operating systems.

Remember to test your application on devices that support high contrast mode to ensure a smooth user experience for all users.

#flutter #accessibility
---
layout: post
title: "MediaQuery systemUIModeChanged in Flutter"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

In Flutter, the [`MediaQuery`](https://api.flutter.dev/flutter/widgets/MediaQuery-class.html) class provides a way to access the responsive dimensions and attributes of your app. One common scenario is handling changes in the system UI mode, such as dark mode or light mode. 

When the system UI mode changes, you can update your app's UI to match the new mode. Flutter provides the `systemUIModeChanged` property in the `MediaQuery` class to detect these changes and trigger the necessary updates.

## Detecting System UI Mode Changes

To detect changes in the system UI mode, you can use the `MediaQueryData.systemBrightness` attribute. This attribute returns the current brightness mode of the system, which can be `Brightness.light` or `Brightness.dark`.

Here's an example of how you can use the `systemUIModeChanged` property to detect and handle system UI mode changes in Flutter:

```dart
import 'package:flutter/material.dart';

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {

  Brightness _currentBrightness;

  @override
  void initState() {
    super.initState();
    WidgetsBinding.instance.addObserver(SystemUiModeNotifier());
  }

  @override
  void dispose() {
    WidgetsBinding.instance.removeObserver(SystemUiModeNotifier());
    super.dispose();
  }

  void _handleSystemUIModeChange(Brightness brightness) {
    setState(() {
      _currentBrightness = brightness;
    });

    // Apply your custom UI changes based on the brightness mode
    // ...

    print('System UI mode changed to $brightness');
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('System UI Mode'),
        ),
        body: Center(
          child: Text(
            'Current UI mode: ${_currentBrightness ?? 'Unknown'}',
            style: TextStyle(fontSize: 24),
          ),
        ),
      ),
    );
  }
}

class SystemUiModeNotifier extends WidgetsBindingObserver {
  @override
  Future<void> didChangeAppLifecycleState(AppLifecycleState state) async {
    if (state == AppLifecycleState.resumed) {
      final brightness = MediaQueryData.fromWindow(WidgetsBinding.instance.window).systemBrightness;
      // Call the method to handle the system UI mode change
      (_MyAppState as _MyAppState)._handleSystemUIModeChange(brightness);
    }
  }
}

void main() {
  runApp(MyApp());
}
```

In this example, the `SystemUiModeNotifier` class extends `WidgetsBindingObserver` to listen for changes in the app's lifecycle. When the app is resumed (`AppLifecycleState.resumed`), it retrieves the current system brightness using `MediaQueryData.fromWindow()` and calls the `_handleSystemUIModeChange()` method in the parent `MyApp` widget.

The `MyApp` widget contains a `_currentBrightness` property, which is updated and triggers a rebuild whenever the system UI mode changes. You can then apply your desired UI changes based on the brightness mode.

## Conclusion

Using the `systemUIModeChanged` property in `MediaQuery`, you can easily detect and handle changes in the system UI mode in your Flutter app. This allows you to provide a consistent user experience across different system UI settings like dark mode and light mode.
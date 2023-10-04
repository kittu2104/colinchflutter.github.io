---
layout: post
title: "How to listen for device pixel ratio changes using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [mediQuery]
comments: true
share: true
---

In Flutter, you can use the `MediaQuery` and `MediaQueryData` classes to access information about the user's device, including the device pixel ratio. The device pixel ratio is the ratio of the physical pixels on the device's screen to the logical pixels used by Flutter.

Listening for changes in the device pixel ratio can be useful in scenarios where you want to dynamically adapt your app's UI based on the device's screen density. Here's how you can listen for device pixel ratio changes using `MediaQuery` in Flutter:

1. Import the necessary packages:

```dart
import 'package:flutter/material.dart';
```

2. Wrap your root widget with a `MediaQuery` widget:

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MediaQuery(
        data: MediaQueryData(),
        child: MyHomePage(),
      ),
    );
  }
}
```

3. Create a stateful widget for the home page:

```dart
class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  double _devicePixelRatio = 0;

  @override
  void initState() {
    super.initState();
    _devicePixelRatio = MediaQuery.of(context).devicePixelRatio;
    MediaQuery.of(context).addListener(_handlePixelRatioChange);
  }

  @override
  void dispose() {
    MediaQuery.of(context).removeListener(_handlePixelRatioChange);
    super.dispose();
  }

  void _handlePixelRatioChange() {
    setState(() {
      _devicePixelRatio = MediaQuery.of(context).devicePixelRatio;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Device Pixel Ratio'),
      ),
      body: Center(
        child: Text(
          'Current Device Pixel Ratio: $_devicePixelRatio',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

By implementing the code above, you create a Flutter app that listens for changes in the device pixel ratio and updates the UI accordingly. The `initState` method initializes the `_devicePixelRatio` value and adds a listener to the `MediaQuery` for listening to changes. When the device pixel ratio changes, the `_handlePixelRatioChange` method is called, which updates the `_devicePixelRatio` value and triggers a UI update using `setState`.

Remember to dispose of the listener in the `dispose` method to prevent memory leaks.

Now, whenever the device pixel ratio changes on the user's device, the UI of your Flutter app will be updated to display the current device pixel ratio.

#flutter #mediQuery
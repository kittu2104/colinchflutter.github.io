---
layout: post
title: "Responding to changes in device orientation using `MediaQuery`"
description: " "
date: 2023-09-23
tags: [responsive]
comments: true
share: true
---

One important aspect of responsive design is ensuring that your web application or website adjusts and adapts seamlessly to changes in device orientation. Whether a user switches from landscape to portrait or vice versa, you want your content to respond accordingly.

In Flutter, you can easily achieve this by utilizing the `MediaQuery` class. This class provides information about the current device's size, orientation, and more. By accessing the `MediaQueryData` object, you can listen for changes in device orientation and update your UI accordingly.

To get started, you need to import the Flutter material package and define a `StatefulWidget` class for your UI component:

```dart
import 'package:flutter/material.dart';

class OrientationExample extends StatefulWidget {
  @override
  _OrientationExampleState createState() => _OrientationExampleState();
}
```

Within the state class, you can add a listener to detect changes in device orientation. You can do this by overriding the `didChangeDependencies` method, which is called whenever the widget's dependencies change:

```dart
class _OrientationExampleState extends State<OrientationExample> {
  MediaQueryData _mediaQueryData;
  bool _isPortrait;

  @override
  Widget build(BuildContext context) {
    _mediaQueryData = MediaQuery.of(context);
    _isPortrait = _mediaQueryData.orientation == Orientation.portrait;

    return Scaffold(
      body: Container(
        child: Center(
          child: Text(
            _isPortrait ? 'Portrait mode' : 'Landscape mode',
            style: TextStyle(fontSize: 24),
          ),
        ),
      ),
    );
  }

  @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    _mediaQueryData = MediaQuery.of(context);
    _isPortrait = _mediaQueryData.orientation == Orientation.portrait;

    // Add code here to update your UI based on orientation
  }
}
```

In the example above, we access the `MediaQueryData` object by calling `MediaQuery.of(context)`. We then check the value of the `orientation` property, which can be either `Orientation.portrait` or `Orientation.landscape`, and set the `_isPortrait` flag accordingly.

Finally, we update our UI based on the `_isPortrait` value. In this case, we display a simple `Text` widget that either shows "Portrait mode" or "Landscape mode" based on the device's orientation.

Remember to use the `OrientationExample` widget within your app to see the changes in device orientation:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: OrientationExample(),
    );
  }
}

void main() {
  runApp(MyApp());
}
```

With the use of `MediaQuery` and its associated classes, you can easily respond to changes in device orientation and create a more user-friendly and adaptable UI for your Flutter application.

#flutter #responsive-design
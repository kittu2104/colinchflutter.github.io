---
layout: post
title: "MediaQuery.of(context) in Flutter"
description: " "
date: 2023-10-01
tags: [mediquery]
comments: true
share: true
---

When developing a Flutter application, it's important to create a responsive and adaptable user interface that looks great on various devices and screen sizes. One way to achieve this is through the use of `MediaQuery.of(context)`.

`MediaQuery.of(context)` allows you to access media-related information, such as screen size, device orientation, and pixel density. With this information, you can dynamically adjust your UI components to fit different device specifications.

Here's an example of how you can use `MediaQuery.of(context)` in your Flutter code:

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  @override
  Widget build(BuildContext context) {
    final screenSize = MediaQuery.of(context).size;
    final devicePixelRatio = MediaQuery.of(context).devicePixelRatio;
    final orientation = MediaQuery.of(context).orientation;

    return Scaffold(
      appBar: AppBar(
        title: Text('MediaQuery Example'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Screen size: $screenSize'),
            Text('Device pixel ratio: $devicePixelRatio'),
            Text('Orientation: $orientation'),
          ],
        ),
      ),
    );
  }
}
```

In this example, we access `MediaQuery.of(context)` in the `build` method of our widget to retrieve the screen size, device pixel ratio, and orientation. We then display this information using `Text` widgets.

By using `MediaQuery.of(context)` in this way, our UI components can dynamically adjust themselves based on the device's specifications, providing a more seamless and optimal user experience.

Remember to import `package:flutter/material.dart` to use the necessary Flutter widgets and classes.

#flutter #mediquery
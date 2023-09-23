---
layout: post
title: "Using `MediaQueryData` properties for conditional rendering in Flutter"
description: " "
date: 2023-09-22
tags: [Flutter, ResponsiveDesign]
comments: true
share: true
---

One common use case for `MediaQueryData` is conditional rendering, where certain components or layouts are displayed based on the screen size or orientation. Here, we'll look at how to use the properties of `MediaQueryData` for conditional rendering in Flutter.

First, let's access the `MediaQueryData` object by using the `MediaQuery.of(context)` method. This method provides the current `MediaQueryData` associated with the given `BuildContext`.

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final mediaQuery = MediaQuery.of(context);

    return Container(
      child: mediaQuery.orientation == Orientation.portrait
          ? Text('Portrait mode')
          : Text('Landscape mode'),
    );
  }
}
```

In the example above, we access the `orientation` property of the `MediaQueryData` object to determine whether the device is in portrait or landscape mode. Based on the orientation, we conditionally render the appropriate text.

But what if we want to render components based on the actual screen size? For this, we can use the `size` property of `MediaQueryData`.

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final mediaQuery = MediaQuery.of(context);

    return Container(
      child: mediaQuery.size.width <= 600
          ? Text('Small screen')
          : Text('Large screen'),
    );
  }
}
```

In this example, we check the `width` of the `size` property to determine whether the screen size is small or large. We can then render different components accordingly.

By leveraging the properties of `MediaQueryData` like `orientation` and `size`, we can easily create responsive layouts in Flutter. This allows our apps to adapt and provide a great user experience across a wide range of devices.

\#Flutter \#ResponsiveDesign
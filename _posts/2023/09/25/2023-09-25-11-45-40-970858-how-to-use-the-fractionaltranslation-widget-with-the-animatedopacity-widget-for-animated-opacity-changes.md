---
layout: post
title: "How to use the FractionalTranslation widget with the AnimatedOpacity widget for animated opacity changes"
description: " "
date: 2023-09-25
tags: [Flutter, Animation]
comments: true
share: true
---

In Flutter, you can use the `FractionalTranslation` widget along with the `AnimatedOpacity` widget to create animated opacity changes. `FractionalTranslation` allows you to specify a translation transformation to move a child widget by a certain fraction of its parent's size. `AnimatedOpacity` allows you to animate changes in opacity, making a widget gradually appear or disappear.

Here's an example of how you can use `FractionalTranslation` and `AnimatedOpacity` together:

```dart
import 'package:flutter/material.dart';

class OpacityAnimationExample extends StatefulWidget {
  @override
  _OpacityAnimationExampleState createState() => _OpacityAnimationExampleState();
}

class _OpacityAnimationExampleState extends State<OpacityAnimationExample> {
  bool _isVisible = true;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Opacity Animation Example'),
      ),
      body: Center(
        child: GestureDetector(
          onTap: () {
            setState(() {
              _isVisible = !_isVisible;
            });
          },
          child: AnimatedOpacity(
            duration: Duration(milliseconds: 500),
            opacity: _isVisible ? 1.0 : 0.0,
            child: FractionalTranslation(
              translation: Offset(0.0, -0.5),
              child: Container(
                width: 200,
                height: 200,
                color: Colors.blue,
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

In this example, we have a `Center` widget containing a `GestureDetector` as its child. When the user taps on the container, the `_isVisible` variable is toggled, which triggers a rebuild of the UI. The `AnimatedOpacity` widget animates the opacity change, gradually fading the container in or out depending on the value of `_isVisible`.

The `AnimatedOpacity` widget wraps the `FractionalTranslation` widget, which applies a vertical translation to the container, moving it up by half of its own size. This creates a smooth animation when the container appears or disappears.

Remember to wrap your `VisibleOpacity` widget with `FractionalTranslation` to achieve the desired effect.

# Summary

Using the `FractionalTranslation` widget with the `AnimatedOpacity` widget in Flutter allows you to create animated opacity changes. By combining these two widgets, you can achieve smooth transitions and effects in your app's UI. Make sure to adjust the translation and opacity values to suit your specific needs.

#Flutter #Animation
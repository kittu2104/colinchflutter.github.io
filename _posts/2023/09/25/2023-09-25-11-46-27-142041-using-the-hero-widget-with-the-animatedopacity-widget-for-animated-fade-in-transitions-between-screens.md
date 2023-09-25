---
layout: post
title: "Using the Hero widget with the AnimatedOpacity widget for animated fade-in transitions between screens"
description: " "
date: 2023-09-25
tags: [Flutter, Animations]
comments: true
share: true
---

When building a user interface in Flutter, it's important to create smooth and visually pleasing transitions between different screens or widgets. One way to achieve this is by using the **Hero** widget combined with the **AnimatedOpacity** widget to create animated fade-in transitions.

The **Hero** widget allows you to animate the transition of a widget from one screen to another while maintaining visual continuity. It works by identifying two widgets with the same tag on different screens and animating the transition between them.

The **AnimatedOpacity** widget, on the other hand, allows you to animate the opacity of a widget over a specified duration. By combining these two widgets, you can create a fade-in effect when transitioning from one screen to another.

Here's an example of how you can implement this technique:

```dart
import 'package:flutter/material.dart';

class Screen1 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Screen 1'),
      ),
      body: Center(
        child: Hero(
          tag: 'myHeroTag',
          child: Container(
            width: 200,
            height: 200,
            color: Colors.blue,
          ),
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => Navigator.push(
          context,
          MaterialPageRoute(
            builder: (context) => Screen2(),
          ),
        ),
        child: Icon(Icons.arrow_forward),
      ),
    );
  }
}

class Screen2 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Screen 2'),
      ),
      body: Center(
        child: Hero(
          tag: 'myHeroTag',
          child: AnimatedOpacity(
            opacity: 1.0,
            duration: Duration(seconds: 1),
            child: Container(
              width: 200,
              height: 200,
              color: Colors.red,
            ),
          ),
        ),
      ),
    );
  }
}
```

In the example above, we have two screens represented by `Screen1` and `Screen2`. The widget inside the `Hero` widget in `Screen1` is identified with the tag `'myHeroTag'`. When the user taps the `FloatingActionButton`, it navigates to `Screen2` where the same widget is wrapped within the `Hero` widget again. The `AnimatedOpacity` widget is used to animate the opacity of the widget over a duration of 1 second, creating a fade-in effect.

By combining the **Hero** widget with the **AnimatedOpacity** widget, you can easily create smooth and visually appealing fade-in transitions between screens in your Flutter application. This technique helps enhance the user experience and adds a touch of elegance to your app.

#Flutter #Animations
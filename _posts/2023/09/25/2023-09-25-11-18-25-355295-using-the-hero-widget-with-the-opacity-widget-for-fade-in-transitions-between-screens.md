---
layout: post
title: "Using the Hero widget with the Opacity widget for fade-in transitions between screens"
description: " "
date: 2023-09-25
tags: [flutteranimation]
comments: true
share: true
---

![hero_opacity_transition](https://example.com/hero_opacity_transition.png)

In Flutter, the Hero widget is commonly used to create smooth transitions between screens by animating the shared elements. By default, the Hero widget performs a fade-out and fade-in transition for the shared element. However, if you want to achieve a fade-in effect when transitioning to a new screen, you can combine the Hero widget with the Opacity widget.

## The Opacity widget

The Opacity widget allows you to adjust the transparency of its child. It takes a value between 0.0 (completely transparent) and 1.0 (completely opaque). By animating this value, you can create a fade-in effect.

Here's an example of using the Hero widget with the Opacity widget to achieve a fade-in transition between screens:

```dart
Hero(
  tag: 'avatar',
  child: Opacity(
    opacity: 0.0,
    child: CircleAvatar(
      backgroundImage: AssetImage('assets/avatar.png'),
    ),
  ),
)
```

In this example, we have a Hero widget wrapped around a CircleAvatar widget. The Hero widget uses the 'avatar' tag to identify this shared element. The Opacity widget is set initially to 0.0 opacity, making the child completely transparent.

To trigger the fade-in effect, you can animate the opacity value using Flutter's animation framework such as the TweenAnimationBuilder or AnimatedOpacity.

```dart
TweenAnimationBuilder<double>(
  tween: Tween<double>(begin: 0.0, end: 1.0),
  duration: Duration(milliseconds: 500),
  builder: (BuildContext context, double value, Widget child) {
    return Opacity(
      opacity: value,
      child: child,
    );
  },
  child: Hero(
    tag: 'avatar',
    child: CircleAvatar(
      backgroundImage: AssetImage('assets/avatar.png'),
    ),
  ),
)
```

In this code snippet, we use the TweenAnimationBuilder to create an animation that transitions the opacity from 0.0 to 1.0 over a duration of 500 milliseconds. The builder function updates the opacity value and returns the Opacity widget with the desired opacity.

By using the Hero widget in combination with the Opacity widget and an animation, you can achieve a fade-in transition effect when navigating between screens in your Flutter app.

#flutter #flutteranimation
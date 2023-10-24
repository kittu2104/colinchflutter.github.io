---
layout: post
title: "CupertinoPageRoute hero animations in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [references, hero]
comments: true
share: true
---

When building a Flutter app, you have the option to use either `MaterialApp` or `CupertinoApp` as the root widget of your application. Both of these widgets provide navigation capabilities, but they have some differences in terms of the animations used.

In this blog post, we will focus on the hero animations specifically provided by `CupertinoPageRoute` in `MaterialApp` and compare it to the default animation behavior in `CupertinoApp`.

## What are hero animations?

Hero animations are a way to smoothly transition an element from one screen to another when navigating between different routes. This creates a visually pleasing effect where an item, typically an image or a widget, appears to move between screens while maintaining its size and proportions. The hero animation creates an illusion of a seamless transition, providing a better user experience.

## Hero animations in MaterialApp

When using `MaterialApp`, the default navigation transition is based on a fade animation. This means that when navigating between routes, the old route fades out while the new route fades in. While this transition is smooth, it does not provide the specific hero animation effect.

In order to achieve hero animations in `MaterialApp`, you need to explicitly define a `Hero` widget in both the source and destination screens. The `Hero` widget requires a unique `tag` parameter, which is used to match the widget between the two screens. Then, you can specify a `Hero` widget as the child of both the source and destination widgets.

```dart
MaterialApp(
  home: Route1(),
  routes: {
    '/route2': (context) => Route2(),
  },
);

class Route1 extends StatefulWidget {
  @override
  _Route1State createState() => _Route1State();
}

class _Route1State extends State<Route1> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Route 1'),
      ),
      body: GestureDetector(
        onTap: () {
          Navigator.pushNamed(context, '/route2');
        },
        child: Hero(
          tag: 'myHero',
          child: Image.network(
            'https://example.com/my-image.jpg',
            fit: BoxFit.cover,
          ),
        ),
      ),
    );
  }
}

class Route2 extends StatefulWidget {
  @override
  _Route2State createState() => _Route2State();
}

class _Route2State extends State<Route2> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Route 2'),
      ),
      body: GestureDetector(
        onTap: () {
          Navigator.pop(context);
        },
        child: Hero(
          tag: 'myHero',
          child: Image.network(
            'https://example.com/my-image.jpg',
            fit: BoxFit.cover,
          ),
        ),
      ),
    );
  }
}
```

In the above example, when the user taps on the image in `Route1`, they will be navigated to `Route2` with a hero animation effect. The image will smoothly transition from `Route1` to `Route2` while maintaining its size and proportions.

## Hero animations in CupertinoApp

On the other hand, `CupertinoApp` provides a different set of default navigation animations compared to `MaterialApp`. In `CupertinoApp`, hero animations are automatically applied when navigating between routes without the need for explicit `Hero` widgets.

The hero animation in `CupertinoApp` mimics the iOS navigation style, where the screen slides in from the right and slides out to the left. This provides a consistent and native feel to the app for iOS users.

However, if you want to have more control over the hero animation in `CupertinoApp`, you can still use the same approach as in `MaterialApp` by explicitly defining `Hero` widgets with unique tags.

```dart
CupertinoApp(
  home: Route1(),
  routes: {
    '/route2': (context) => Route2(),
  },
);

class Route1 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Route 1')
      ),
      child: GestureDetector(
        onTap: () {
          Navigator.pushNamed(context, '/route2');
        },
        child: Hero(
          tag: 'myHero',
          child: Image.network(
            'https://example.com/my-image.jpg',
            fit: BoxFit.cover,
          ),
        ),
      ),
    );
  }
}

class Route2 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Route 2')
      ),
      child: GestureDetector(
        onTap: () {
          Navigator.pop(context);
        },
        child: Hero(
          tag: 'myHero',
          child: Image.network(
            'https://example.com/my-image.jpg',
            fit: BoxFit.cover,
          ),
        ),
      ),
    );
  }
}
```

In the above example, the hero animation is applied by default when navigating between `Route1` and `Route2` in `CupertinoApp`. The image smoothly transitions with the slide animation.

## Conclusion

In summary, `MaterialApp` and `CupertinoApp` provide different default navigation and animation behaviors. While `MaterialApp` requires explicit `Hero` widgets to achieve hero animations, `CupertinoApp` applies a slide animation automatically. However, in both cases, you can still define `Hero` widgets with unique tags to have more control over the hero animation effect.

Understanding the differences and capabilities of both `MaterialApp` and `CupertinoApp` allows you to create a more immersive and visually appealing user experience in your Flutter applications.

#references: 
- Hero animations in Flutter: [https://flutter.dev/docs/development/ui/animations/hero-animations](https://flutter.dev/docs/development/ui/animations/hero-animations)
- CupertinoPageRoute class documentation: [https://api.flutter.dev/flutter/cupertino/CupertinoPageRoute-class.html](https://api.flutter.dev/flutter/cupertino/CupertinoPageRoute-class.html)
- MaterialApp class documentation: [https://api.flutter.dev/flutter/material/MaterialApp-class.html](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- CupertinoApp class documentation: [https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)

#flutter #hero-animations
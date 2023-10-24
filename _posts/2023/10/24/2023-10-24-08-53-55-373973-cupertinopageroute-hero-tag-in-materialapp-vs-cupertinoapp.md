---
layout: post
title: "CupertinoPageRoute hero tag in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [appdevelopment]
comments: true
share: true
---

When developing mobile applications, user experience plays a crucial role in creating a seamless and visually appealing interface. To achieve this, Flutter provides different types of page transition animations. In this blog post, we will explore how to use the `heroTag` property for page transitions in two different scenarios: within the `MaterialApp` and `CupertinoApp` widgets.

## Table of Contents
- [Introduction](#introduction)
- [Using hero tag in MaterialApp](#using-hero-tag-in-materialapp)
- [Using hero tag in CupertinoApp](#using-hero-tag-in-cupertinoapp)
- [Conclusion](#conclusion)

## Introduction

Flutter provides two main types of app widgets, `MaterialApp` and `CupertinoApp`, which allow developers to define the overall look and feel of their application based on the respective design language of Android and iOS. Both widgets offer a way to specify page transitions when navigating between screens.

## Using hero tag in MaterialApp

When using the `MaterialApp` widget, developers can utilize the `CupertinoPageRoute` class along with the `heroTag` property to create visually stunning page transitions. The `heroTag` property allows developers to specify a unique identifier for the hero animation, ensuring that the same hero animation is applied when transitioning between different screens.

Here's an example of how to use `heroTag` within a `MaterialApp`:

```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => SecondScreen(),
    settings: RouteSettings(name: '/second'),
  ),
);
```

And in the second screen:

```dart
class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Second Screen'),
      ),
      body: Hero(
        tag: 'avatar',
        child: Image.asset('assets/avatar.png'),
      ),
    );
  }
}
```

In the above example, the `hero` widget in the second screen is given the tag 'avatar', so when transitioning between screens, the image will smoothly animate from the first to the second screen.

## Using hero tag in CupertinoApp

Similarly, when using the `CupertinoApp` widget, developers can still make use of the `heroTag` property within the `CupertinoPageRoute` class to implement visually appealing page transitions. The process is quite similar to that of the `MaterialApp` example.

```dart
Navigator.push(
  context,
  CupertinoPageRoute(
    builder: (context) => SecondScreen(),
    settings: RouteSettings(name: '/second'),
  ),
);
```

And in the second screen:

```dart
class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Second Screen'),
      ),
      child: Hero(
        tag: 'avatar',
        child: Image.asset('assets/avatar.png'),
      ),
    );
  }
}
```

As shown in the example, the `heroTag` property is used within the `Hero` widget to create the desired animation effect when transitioning between screens in a Flutter app built with the `Cupertino` design language.

## Conclusion

Using the `heroTag` property along with the appropriate app widget, whether it's `MaterialApp` or `CupertinoApp`, allows developers to create visually stunning page transitions in Flutter applications. By specifying a unique identifier for the hero animation, developers can ensure consistent and visually appealing screen transitions, thus enhancing the overall user experience.

Feel free to experiment with different `heroTag` values and animations to bring your Flutter app to life!

\#flutter #appdevelopment
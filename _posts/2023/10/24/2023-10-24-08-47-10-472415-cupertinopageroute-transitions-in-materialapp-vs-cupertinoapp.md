---
layout: post
title: "CupertinoPageRoute transitions in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When building a Flutter app, you have the option to use either the `MaterialApp` or `CupertinoApp` widget as the root of your application. These widgets provide different design philosophies based on Google's Material Design guidelines and Apple's Cupertino design guidelines, respectively.

One of the key differences between the two is how page transitions are handled. The `MaterialApp` widget uses `MaterialPageRoute`, while the `CupertinoApp` widget uses `CupertinoPageRoute`. Let's take a closer look at these transitions and see how they differ.

## MaterialPageRoute

The `MaterialPageRoute` is the default transition used in a `MaterialApp`. It provides a visual cue to the user that they are moving to a different page within the app. The transition typically consists of a slide from right to left or left to right, depending on the language direction of the app.

Here's an example of how to use `MaterialPageRoute` when navigating to a new page:

```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => MyNewScreen(),
  ),
);
```

By default, the `MaterialPageRoute` transition provides a smooth animation between pages, giving your app an intuitive flow.

## CupertinoPageRoute

In contrast, the `CupertinoPageRoute` is the default transition used in a `CupertinoApp`. It follows Apple's design guidelines and provides a different visual experience compared to the `MaterialPageRoute`. It typically features a slide-up animation to present a new page and a slide-down animation when dismissing it.

Here's an example of how to use `CupertinoPageRoute` when navigating to a new page:

```dart
Navigator.push(
  context,
  CupertinoPageRoute(
    builder: (context) => MyNewScreen(),
  ),
);
```

The `CupertinoPageRoute` transition is designed to match the look and feel of iOS apps, providing a seamless and consistent user experience for Apple device users.

## Choosing the Right Transition

Whether to use `MaterialPageRoute` or `CupertinoPageRoute` depends on the design language you want to adopt in your app. If you are building a cross-platform app or following Google's Material Design guidelines, using `MaterialPageRoute` in a `MaterialApp` is a suitable choice.

On the other hand, if you are targeting iOS devices and want to follow Apple's design guidelines, using `CupertinoPageRoute` in a `CupertinoApp` is the way to go.

Remember, you can also customize the page transitions by creating your own custom route transitions by extending `PageRoute` and implementing your desired animation.

In conclusion, the choice between `CupertinoPageRoute` and `MaterialPageRoute` depends on the design language and target platform of your Flutter app. Both offer visually appealing transitions that enhance the user experience, so make your decision based on the overall aesthetic and feel of your application.

#flutter #ui
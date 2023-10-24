---
layout: post
title: "Cupertino page route customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing mobile applications with Flutter, you have the option to choose between `MaterialApp` and `CupertinoApp` as the root widget for your app. These two widgets provide different design languages that are commonly used on Android and iOS platforms respectively. 

One aspect of app development that might differ between `MaterialApp` and `CupertinoApp` is the customization of page routes. In this blog post, we will explore how page route customization differs between these two widgets.

## 1. MaterialApp

`MaterialApp` is typically used to create apps with a Material Design look and feel. When it comes to page route customization, `MaterialApp` provides several options.

### Default Page Transition

By default, `MaterialApp` uses a slide animation when navigating between screens. This default behavior is suitable for most apps and can be easily customized if needed.

### Custom Page Transitions

If you want to create more complex or custom page transitions, you can use the `PageRouteBuilder` class. This class allows you to define different animation styles, such as fade, scale, and more. With `PageRouteBuilder`, you have full control over how your pages transition.

Here's an example of a custom page transition using the `MaterialPageRoute`:

```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => MyCustomPage()),
);
```

### Named Routes

Using named routes with `MaterialApp` is another way to customize page routes. By defining named routes in your app's `routes` property, you can easily navigate to specific screens using their names.

```dart
MaterialApp(
  routes: {
    '/home': (context) => HomePage(),
    '/details': (context) => DetailsPage(),
  },
);
```

Navigating to a named route is as simple as using `Navigator.pushNamed(context, '/details')`.

## 2. CupertinoApp

In contrast to `MaterialApp`, `CupertinoApp` is used to create apps with an iOS-like design. Let's take a look at how page route customization works with `CupertinoApp`.

### Default Page Transition

Similar to `MaterialApp`, `CupertinoApp` also uses a slide animation as the default page transition effect.

### Custom Page Transitions

If you want to create custom page transitions with `CupertinoApp`, you can use the `CupertinoPageRoute` class. This allows you to define custom transition effects that resemble those found in iOS apps.

```dart
Navigator.push(
  context,
  CupertinoPageRoute(builder: (context) => MyCustomPage()),
);
```

### Named Routes

Just like with `MaterialApp`, you can also use named routes with `CupertinoApp` for easy navigation.

```dart
CupertinoApp(
  routes: {
    '/home': (context) => HomePage(),
    '/details': (context) => DetailsPage(),
  },
);
```

Navigation to a named route in `CupertinoApp` can be done using `Navigator.pushNamed(context, '/details')`.

## Conclusion

Both `MaterialApp` and `CupertinoApp` provide options for customizing page routes in your Flutter app. Whether you choose to use the Material Design or iOS design language, you can achieve the desired page transition effects and easily navigate between screens.

By understanding the differences between these two widgets, you can make an informed decision on which one to use based on your app's specific requirements.

## References

- Flutter Documentation: [https://flutter.dev/docs](https://flutter.dev/docs)
- Material Design Guidelines: [https://material.io](https://material.io)
- Cupertino Design Guidelines: [https://developer.apple.com/design/human-interface-guidelines](https://developer.apple.com/design/human-interface-guidelines)
---
layout: post
title: "MediaQuery useInheritedMediaQuery in Flutter"
description: " "
date: 2023-10-01
tags: [InheritedWidget]
comments: true
share: true
---

In Flutter, **`MediaQuery`** is a powerful tool that allows you to access the current **media query data** such as **display size**, **orientation**, and more. By default, `MediaQuery` retrieves the data for the current widget tree, but sometimes you might need to access this data in a descendant widget that is not directly connected to the parent widget. This is where **`InheritedMediaQuery`** comes into play.

## What is InheritedWidget?

`InheritedMediaQuery` is a subclass of **`InheritedWidget`**. It allows you to propagate data from a parent widget to its descendants throughout the widget tree. This is useful when you want to share data between multiple widgets without passing it explicitly through constructors.

## How to use InheritedMediaQuery?

Using `InheritedMediaQuery` is a two-step process. First, you need to define a subclass of `InheritedWidget` to hold the data you want to share. In this case, we are interested in accessing the `MediaQueryData`.

```dart
class MyMediaQuery extends InheritedWidget {
  final MediaQueryData mediaQueryData;

  MyMediaQuery({
    Key key,
    @required this.mediaQueryData,
    @required Widget child,
  }) : super(key: key, child: child);

  static MyMediaQuery of(BuildContext context) {
    return context.dependOnInheritedWidgetOfExactType<MyMediaQuery>();
  }

  @override
  bool updateShouldNotify(MyMediaQuery oldWidget) {
    return mediaQueryData != oldWidget.mediaQueryData;
  }
}
```

In the example above, `MyMediaQuery` is a subclass of `InheritedWidget` that encapsulates the `mediaQueryData` field. It also provides a `static` method called `of(BuildContext context)`, which will be used to access the `MyMediaQuery` instance from descendant widgets.

Next, wrap your app's root widget with `MyMediaQuery`:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MyMediaQuery(
      mediaQueryData: MediaQuery.of(context),
      child: MaterialApp(
        title: 'My App',
        home: HomeScreen(),
      ),
    );
  }
}
```

In the example above, we pass the `mediaQueryData` from the `MediaQuery.of(context)` method to the `MyMediaQuery` constructor.

Finally, to access the `MediaQueryData`, use `MyMediaQuery.of(context).mediaQueryData` in any descendant widget:

```dart
class SomeWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final mediaQuery = MyMediaQuery.of(context).mediaQueryData;

    return Container(
      height: mediaQuery.size.height,
      width: mediaQuery.size.width,
      child: Text('Some Widget'),
    );
  }
}
```

In the example above, we access the `mediaQueryData` using `MyMediaQuery.of(context).mediaQueryData`. This gives us access to the current `MediaQueryData` within the descendant widget.

Using `InheritedMediaQuery` allows you to easily share the `MediaQueryData` with any widget in the subtree, making it a powerful tool for building responsive and adaptive user interfaces in Flutter.

That's it! You can now utilize `InheritedMediaQuery` to access `MediaQueryData` throughout your Flutter widget tree.

#Flutter #InheritedWidget
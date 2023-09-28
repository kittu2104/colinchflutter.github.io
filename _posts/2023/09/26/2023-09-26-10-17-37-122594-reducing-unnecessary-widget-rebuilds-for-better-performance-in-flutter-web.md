---
layout: post
title: "Reducing unnecessary widget rebuilds for better performance in Flutter web"
description: " "
date: 2023-09-26
tags: [techblog, flutterweb]
comments: true
share: true
---

In the world of Flutter web development, performance is paramount. As users navigate through our web applications, we want to ensure smooth and responsive experiences. One area that can impact performance is unnecessary widget rebuilds. In this blog post, we will explore some techniques to reduce widget rebuilds and improve the overall performance of our Flutter web apps.

## 1. Use `const` Widgets

In Flutter, the `const` keyword is used to create "constant" widgets. These widgets have properties whose values are known at compile-time and do not change during runtime. By using `const` widgets, Flutter can optimize and skip unnecessary rebuilds. However, keep in mind that only simple, non-dynamic widgets can be marked as `const`.

Here's an example:

```dart
class MyWidget extends StatelessWidget {
  const MyWidget({Key key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return const Text("Hello, World!"); // Marking Text widget as `const`
  }
}
```

## 2. Utilize `const` Constructors

In addition to marking individual widgets with `const`, we can also use `const` constructors provided by some of the built-in Flutter widgets. These constructors allow us to create multiple `const` widgets without unnecessary rebuilds.

For instance, if we need to create a `ListView` with a fixed set of children, we can use the `ListView.builder` constructor with `const` widgets inside the `itemBuilder`:

```dart
ListView.builder(
  itemCount: 3,
  itemBuilder: (context, index) => const MyWidget(), // MyWidget is marked as `const`
)
```

## 3. Implement `shouldRepaint` in Custom Painters

When working with custom painters in Flutter, implementing the `shouldRepaint` method can help reduce unnecessary repaints. The `shouldRepaint` method is called whenever the custom painter is scheduled to be repainted. By returning `false` when the new and old values are identical, we can prevent unnecessary rebuilds.

```dart
class MyCustomPainter extends CustomPainter {
  @override
  bool shouldRepaint(MyCustomPainter oldDelegate) {
    // Implement your comparison logic here and return true only when repaint is required
    return false; // Prevents unnecessary rebuilds
  }

  @override
  void paint(Canvas canvas, Size size) {
    // Custom painting logic
  }

  @override
  bool shouldRebuildSemantics(MyCustomPainter oldDelegate) => false;
}
```

## 4. Use `Key` to Preserve Widget State

In some cases, we might have widgets that share the same type and properties but need to maintain different states. To preserve the state of such widgets across rebuilds, it is essential to provide a unique `Key` for each instance.

```dart
class MyStatefulWidget extends StatefulWidget {
  const MyStatefulWidget({Key key}) : super(key: key);

  @override
  _MyStatefulWidgetState createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  int _counter = 0;

  @override
  Widget build(BuildContext context) {
    return Text("Counter: $_counter");
  }
}
```

By using a unique `Key` for each instance of `MyStatefulWidget`, Flutter will only rebuild the specific widget that needs updating, instead of rebuilding all instances.

## Conclusion

By applying these techniques, we can reduce unnecessary widget rebuilds and optimize the performance of our Flutter web apps. It's crucial to be mindful of when and where to use `const` widgets and constructors, implement `shouldRepaint` for custom painters, and utilize `Key` to preserve widget state. With these optimizations in place, our Flutter web applications can deliver a smooth and responsive user experience.

#techblog #flutterweb
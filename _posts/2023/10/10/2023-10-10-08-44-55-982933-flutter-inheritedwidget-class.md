---
layout: post
title: "Flutter InheritedWidget class"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

InheritedWidget is a powerful and fundamental class in Flutter that facilitates the sharing of data across the widget tree. It serves as a way to propagate data down the widget tree without having to pass it manually to each widget.

## What is InheritedWidget?

InheritedWidget is a subclass of StatefulWidget and is designed to hold data that can be accessed by descendant widgets. It wraps the entire widget tree under it and provides access to the data to any widget that calls [InheritedWidget.of(context)](https://api.flutter.dev/flutter/widgets/InheritedWidget/of.html).

## How to use InheritedWidget?

To utilize the power of InheritedWidget, you need to follow these steps:

### 1. Create an InheritedWidget subclass

Create your own subclass by extending the InheritedWidget class. This subclass will hold the data that you want to share across the widget tree.

```dart
class MyInheritedWidget extends InheritedWidget {
  final String sharedData;

  MyInheritedWidget({required this.sharedData, required Widget child}) : super(child: child);

  @override
  bool updateShouldNotify(covariant MyInheritedWidget oldWidget) {
    return sharedData != oldWidget.sharedData;
  }

  static MyInheritedWidget of(BuildContext context) {
    return context.dependOnInheritedWidgetOfExactType<MyInheritedWidget>()!;
  }
}
```

### 2. Use the InheritedWidget in your widget tree

Wrap the widget tree with your custom InheritedWidget subclass and provide the data that you want to share.

```dart
MyInheritedWidget(
  sharedData: 'Hello World',
  child: MyApp(),
)
```

### 3. Accessing the shared data

Use the [InheritedWidget.of(context)](https://api.flutter.dev/flutter/widgets/InheritedWidget/of.html) method to retrieve the shared data in any widget that is a descendant of the InheritedWidget.

```dart
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final sharedData = MyInheritedWidget.of(context).sharedData;

    return Text(sharedData);
  }
}
```

## Why use InheritedWidget?

InheritedWidget offers several benefits, some of which include:

- Efficient data propagation: InheritedWidget smartly rebuilds only the widgets that depend on the shared data when it changes, resulting in optimized performance.
- Simplified data sharing: It eliminates the need to explicitly pass data through widget constructors, reducing boilerplate code.
- Scoped data sharing: You can provide different instances of InheritedWidgets at different levels of the widget tree, allowing data to be scoped appropriately.

## Conclusion

InheritedWidget is a powerful class in Flutter that enables the sharing of data across the widget tree. By utilizing InheritedWidget, you can efficiently propagate data down the widget tree and reduce the complexity of passing data manually between widgets.

So, next time you need to share data across your Flutter app, consider using the InheritedWidget class and take advantage of its powerful capabilities.

#flutter #flutterdevelopment
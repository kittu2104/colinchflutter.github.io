---
layout: post
title: "How to use inherited MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [inheritedwidget]
comments: true
share: true
---

In Flutter, the `MediaQuery` class provides information about the current device and screen dimensions. It allows you to retrieve properties such as the screen size, orientation, pixel density, and more. While you can access this information directly using the `MediaQuery.of(context)` method, there are cases where you may need to pass this information down the widget tree without explicitly calling `MediaQuery.of(context)` at each level. This is where the `InheritedWidget` and `InheritedModel` come into play.

## Inheriting MediaQuery Using InheritedWidget

To inherit the `MediaQuery` throughout your widget tree without explicitly calling `MediaQuery.of(context)`, you can use the `InheritedWidget` class. Here's a step-by-step guide on how to do that:

1. Create a new class that extends `InheritedWidget`. This class will be responsible for holding the `MediaQueryData` and passing it down the widget tree.

```dart
class MediaQueryInherited extends InheritedWidget {
  final MediaQueryData mediaQueryData;

  MediaQueryInherited({
    required this.mediaQueryData,
    required Widget child,
  }) : super(child: child);

  // Method to check if the widget should update when the data changes

  @override
  bool updateShouldNotify(covariant MediaQueryInherited oldWidget) {
    return oldWidget.mediaQueryData != mediaQueryData;
  }

  // Method to access the inherited data

  static MediaQueryInherited? of(BuildContext context) {
    return context.dependOnInheritedWidgetOfExactType<MediaQueryInherited>();
  }
}
```

2. Place the `MediaQuery` widget higher up in your widget tree and wrap it with the newly created `MediaQueryInherited` widget.

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MediaQueryInherited(
      mediaQueryData: MediaQuery.of(context),
      child: MaterialApp(
        title: 'Inherited MediaQuery Example',
        home: HomePage(),
      ),
    );
  }
}
```

3. In any widget that needs access to the `MediaQuery` data, use the `MediaQueryInherited.of(context)` method to retrieve the inherited data.

```dart
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final mediaQueryData = MediaQueryInherited.of(context)?.mediaQueryData;
    
    // Use the mediaQueryData for your calculations or rendering

    return Container(
      width: mediaQueryData?.size.width,
      height: mediaQueryData?.size.height,
      child: Text('Example Widget'),
    );
  }
}
```

By following these steps, you can access the `MediaQuery` data anywhere in your widget tree without explicitly calling `MediaQuery.of(context)`.

## Conclusion

Using the `InheritedWidget` approach, you can easily pass down the `MediaQuery` data throughout your widget tree without the need to call `MediaQuery.of(context)` repeatedly. This approach makes your code cleaner and more efficient.

#flutter #inheritedwidget
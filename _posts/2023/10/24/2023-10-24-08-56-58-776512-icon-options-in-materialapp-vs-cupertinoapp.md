---
layout: post
title: "Icon options in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When working with Flutter, you have the flexibility to choose between different widget libraries for building your user interface. Two popular options are `MaterialApp` and `CupertinoApp`. These libraries provide a set of default widgets and themes that follow the design principles of Material Design and Cupertino respectively.

One key difference between these libraries is the set of icons they provide out of the box. In this blog post, we will explore the icon options available in `MaterialApp` and `CupertinoApp`.

## Icons in MaterialApp

When using the `MaterialApp` widget, you have access to the Material Design icon set. This icon set includes a large variety of icons that you can use in your application. These icons are available through the `Icons` class provided by Flutter.

Here's an example of how you can use the `Icons` class to display an icon in your `MaterialApp`:

```dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('MaterialApp Icon Example'),
        ),
        body: Center(
          child: Icon(
            Icons.star,
            size: 48,
            color: Colors.yellow,
          ),
        ),
      ),
    );
  }
}
```

In the code example above, we imported the `flutter/material.dart` package and used the `Icon` widget to display a star-shaped icon from the `Icons` class. We also specified the size and color of the icon.

## Icons in CupertinoApp

On the other hand, if you choose to use the `CupertinoApp` widget, you will have access to the Cupertino icon set which follows the design principles of iOS. This icon set is available through the `CupertinoIcons` class provided by Flutter.

Here's an example of how you can use the `CupertinoIcons` class to display an icon in your `CupertinoApp`:

```dart
import 'package:flutter/cupertino.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      home: CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          middle: Text('CupertinoApp Icon Example'),
        ),
        child: Center(
          child: Icon(
            CupertinoIcons.star,
            size: 48,
            color: CupertinoColors.systemYellow,
          ),
        ),
      ),
    );
  }
}
```

In the code example above, we imported the `flutter/cupertino.dart` package and used the `Icon` widget to display a star-shaped icon from the `CupertinoIcons` class. We also specified the size and color of the icon.

## Conclusion

Both `MaterialApp` and `CupertinoApp` provide their own sets of icons that align with their respective design principles. It's important to choose the appropriate widget library based on the platform you are targeting and the desired user experience.

Please keep in mind that the above examples are just a glimpse of the available icon options. You can explore the full set of icons provided by `Icons` and `CupertinoIcons` classes in the Flutter documentation.

Happy icon exploration in your Flutter projects! 😊

**References:**

- [Flutter Material Design documentation](https://flutter.dev/docs/development/ui/widgets/material)
- [Flutter Cupertino Design documentation](https://flutter.dev/docs/development/ui/widgets/cupertino)
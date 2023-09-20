---
layout: post
title: "Applying custom scroll physics to CupertinoPageScaffold and CupertinoActivityIndicator in Flutter"
description: " "
date: 2023-09-20
tags: [flutter, scrollphysics]
comments: true
share: true
---

In Flutter, the `CupertinoPageScaffold` widget provides a native iOS-like layout for your app screens, while `CupertinoActivityIndicator` displays a spinning progress indicator. By default, these widgets come with predefined scroll physics and animation behavior. However, you might want to apply custom scroll physics to provide a more interactive and unique user experience. In this blog post, we will walk you through the process of applying custom scroll physics to `CupertinoPageScaffold` and using it in combination with `CupertinoActivityIndicator`.

## Customizing Scroll Physics

1. Import the necessary libraries:

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/widgets.dart';
```

2. Create a custom scroll physics class that extends `ScrollPhysics`:

```dart
class CustomScrollPhysics extends ScrollPhysics {
  const CustomScrollPhysics({ScrollPhysics? parent}) : super(parent: parent);

  @override
  CustomScrollPhysics applyTo(ScrollPhysics? ancestor) {
    return CustomScrollPhysics(parent: buildParent(ancestor));
  }

  @override
  double applyPhysicsToUserOffset(ScrollMetrics position, double offset) {
    // Apply your custom scroll physics logic here
    // Manipulate the offset value based on your requirements
    return offset;
  }
}
```

3. Use the custom scroll physics in `CupertinoPageScaffold`:

```dart
CupertinoPageScaffold(
  navigationBar: CupertinoNavigationBar(
    // Navigation bar properties
  ),
  child: ScrollConfiguration(
    behavior: ScrollBehavior().copyWith(
      physics: const CustomScrollPhysics(),
    ),
    child: ListView(
      // ListView content
    ),
  ),
)
```

## Combining with CupertinoActivityIndicator

1. Import the necessary libraries:

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/widgets.dart';
```

2. Use a `NotificationListener` widget to detect scroll events:

```dart
bool _isLoading = false; // Track if data is being loaded

ListView(
  children: [
    // Your list items
    NotificationListener<ScrollNotification>(
      onNotification: (notification) {
        if (notification is ScrollEndNotification &&
            notification.metrics.extentAfter == 0) {
          // Reach the end of the list
          loadData(); // Load more data
          return true;
        }
        return false;
      },
      child: CupertinoActivityIndicator(
        radius: 16.0,
        animating: _isLoading,
      ),
    ),
  ],
)
```

3. Implement the `loadData` method to load more data and update the `_isLoading` state:

```dart
void loadData() {
  setState(() {
    _isLoading = true;
    // Load more data here
    // Once the data is loaded, set _isLoading to false
  });
}
```

With the code snippets provided in this blog post, you can now apply custom scroll physics to `CupertinoPageScaffold` and use it in combination with `CupertinoActivityIndicator` to create a more engaging user experience in your Flutter app.

#flutter #scrollphysics
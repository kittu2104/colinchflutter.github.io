---
layout: post
title: "Building a swipeable carousel using ListView in Flutter."
description: " "
date: 2023-09-15
tags: [Carousel]
comments: true
share: true
---

Flutter is a cross-platform UI toolkit that allows developers to create beautiful apps for mobile, web, and desktop from a single codebase. In this tutorial, we will learn how to build a swipeable carousel using ListView in Flutter.

## Prerequisites

Before we begin, make sure you have Flutter and Dart installed on your system. You can download Flutter from the official Flutter website and follow the installation instructions.

## Getting Started

To get started, create a new Flutter project using the following command:

```shell
flutter create carousel_example
```

Navigate to the project directory:

```shell
cd carousel_example
```

Open the `lib/main.dart` file and replace its contents with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(CarouselApp());
}

class CarouselApp extends StatelessWidget {
  final List<String> carouselItems = [
    'Item 1',
    'Item 2',
    'Item 3',
    'Item 4',
    'Item 5',
  ];

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Swipeable Carousel'),
        ),
        body: ListView.builder(
          itemCount: carouselItems.length,
          itemBuilder: (context, index) {
            final item = carouselItems[index];
            return ListTile(
              title: Text(item),
            );
          },
        ),
      ),
    );
  }
}
```

## Explanation

In the above code, we have created a Flutter app with a `CarouselApp` class as the root widget. Inside the `build` method, we have used `MaterialApp` and `Scaffold` to set up the basic app structure. We have also added an `AppBar` with the title "Swipeable Carousel".

Inside the `body`, we have used the `ListView.builder` widget to create a scrollable list of items. The `itemCount` property specifies the number of items in the list, and the `itemBuilder` callback method is called for each item in the list. We have used `ListTile` as the list item widget to display each item.

## Adding Swipe Gesture

To make the list items swipeable, we can wrap the `ListTile` widget inside a `Dismissible` widget. Update the `itemBuilder` callback in the code above like this:

```dart
itemBuilder: (context, index) {
  final item = carouselItems[index];
  return Dismissible(
    key: Key(item),
    onDismissed: (direction) {
      // Handle swipe to dismiss
    },
    child: ListTile(
      title: Text(item),
    ),
  );
},
```

In the code above, we have added the `Dismissible` widget as the parent of the `ListTile`. The `key` property is set to a unique value for each item, and the `onDismissed` callback is called when the item is swiped and dismissed.

## Conclusion

In this tutorial, we have learned how to build a swipeable carousel using ListView in Flutter. We have created a basic app structure and added a scrollable list of items. We have also made the list items swipeable by wrapping them inside a `Dismissible` widget. You can now further customize the carousel by adding images or other UI elements to the list items.

#Flutter #Carousel
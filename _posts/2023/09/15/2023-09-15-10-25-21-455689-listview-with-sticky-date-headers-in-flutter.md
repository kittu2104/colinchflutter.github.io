---
layout: post
title: "ListView with sticky date headers in Flutter."
description: " "
date: 2023-09-15
tags: [ListView, StickyHeaders]
comments: true
share: true
---

When working on a Flutter app, you may often come across the need to display a list of items categorized by date, with sticky headers to separate the items for each date. In this blog post, we will explore how to implement a ListView with sticky date headers in Flutter using the `sticky_headers` package.

## Installing the `sticky_headers` Package

To get started, we need to add the `sticky_headers` package to our Flutter project. Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  sticky_headers: ^0.2.0
```

Save the file, and in the terminal, run the following command to download and install the package:

```bash
flutter pub get
```

## Implementing the ListView

Here is a complete example of how to use the `sticky_headers` package to create a ListView with sticky date headers:

```dart
import 'package:flutter/material.dart';
import 'package:sticky_headers/sticky_headers.dart';

class MyListView extends StatelessWidget {
  final List<String> items = [
    "Item 1",
    "Item 2",
    "Item 3",
    // ...
  ];

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: items.length,
      itemBuilder: (context, index) {
        if (index == 0 || items[index - 1] != items[index]) {
          return StickyHeader(
            header: Container(
              height: 50,
              color: Colors.grey[300],
              alignment: Alignment.centerLeft,
              padding: EdgeInsets.symmetric(horizontal: 16),
              child: Text(
                "Date Header",
                style: TextStyle(
                  fontWeight: FontWeight.bold,
                ),
              ),
            ),
            content: ListTile(
              title: Text(items[index]),
            ),
          );
        } else {
          return ListTile(
            title: Text(items[index]),
          );
        }
      },
    );
  }
}
```

In this example, we have a list of items represented by the `items` list. We use the `ListView.builder` to build the list dynamically based on the number of items. Inside the `itemBuilder`, we check if the current item is the first item or if it is different from the previous item. If it is, we create a `StickyHeader` widget with a header that displays the date. Otherwise, we simply create a `ListTile` for the item.

## Conclusion

Implementing a ListView with sticky date headers in Flutter is made easy with the `sticky_headers` package. By using the code example provided, you can create a visually appealing and user-friendly list that organizes items by date. Feel free to customize the code to fit your specific requirements.

#Flutter #ListView #StickyHeaders
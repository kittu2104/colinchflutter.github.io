---
layout: post
title: "ListView with sticky headers and sticky footers in Flutter."
description: " "
date: 2023-09-15
tags: [flutterdev, stickyheaders]
comments: true
share: true
---

One common requirement in mobile app development is to implement a list with sticky headers and sticky footers. This feature allows users to scroll through a long list while keeping certain items, such as headers and footers, fixed at the top or bottom of the screen. In Flutter, we can achieve this functionality using the **flutter_sticky_header** package.

## Installation

To begin, add the **flutter_sticky_header** package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_sticky_header: ^0.5.0
```

Then, run `flutter pub get` to download and install the package.

## Usage

### Import the Package

```dart
import 'package:flutter_sticky_header/flutter_sticky_header.dart';
```

### Create ListView with Sticky Headers and Sticky Footers

To create a ListView with sticky headers and sticky footers, we need to use the `SliverStickyHeader` widget provided by the **flutter_sticky_header** package. Let's see an example of how to implement this feature:

```dart
class StickyHeaderListView extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Sticky Header ListView'),
      ),
      body: CustomScrollView(
        slivers: <Widget>[
          SliverStickyHeader(
            header: Container(
              height: 50,
              color: Colors.blue,
              alignment: Alignment.center,
              child: Text(
                'Header 1',
                style: TextStyle(color: Colors.white, fontSize: 20),
              ),
            ),
            sliver: SliverList(
              delegate: SliverChildListDelegate([
                ListTile(title: Text('Item 1')),
                ListTile(title: Text('Item 2')),
                ListTile(title: Text('Item 3')),
                // ...
              ]),
            ),
          ),
          SliverStickyHeader(
            header: Container(
              height: 50,
              color: Colors.orange,
              alignment: Alignment.center,
              child: Text(
                'Header 2',
                style: TextStyle(color: Colors.white, fontSize: 20),
              ),
            ),
            sliver: SliverList(
              delegate: SliverChildListDelegate([
                ListTile(title: Text('Item 4')),
                ListTile(title: Text('Item 5')),
                ListTile(title: Text('Item 6')),
                // ...
              ]),
            ),
          ),
          SliverStickyHeader(
            footer: Container(
              height: 50,
              color: Colors.green,
              alignment: Alignment.center,
              child: Text(
                'Footer 1',
                style: TextStyle(color: Colors.white, fontSize: 20),
              ),
            ),
            sliver: SliverList(
              delegate: SliverChildListDelegate([
                ListTile(title: Text('Item 7')),
                ListTile(title: Text('Item 8')),
                ListTile(title: Text('Item 9')),
                // ...
              ]),
            ),
          ),
        ],
      ),
    );
  }
}
```

In the above code, we create a `CustomScrollView` with multiple `SliverStickyHeader` widgets. Each `SliverStickyHeader` contains a header and a sliver, which can be a `SliverList`, or any other type of sliver. We can also add a footer to each `SliverStickyHeader` by setting the `footer` property.

## Conclusion

By using the **flutter_sticky_header** package, we can easily create a ListView with sticky headers and sticky footers in Flutter. This feature enhances the user experience by allowing them to navigate through long lists while keeping important items fixed at the top or bottom. Explore the package documentation for more customization options and additional features.

#flutter #flutterdev #stickyheaders
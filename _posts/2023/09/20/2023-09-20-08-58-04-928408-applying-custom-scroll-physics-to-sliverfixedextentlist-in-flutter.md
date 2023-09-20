---
layout: post
title: "Applying custom scroll physics to SliverFixedExtentList in Flutter"
description: " "
date: 2023-09-20
tags: [scrollphysics]
comments: true
share: true
---

In Flutter, the `SliverFixedExtentList` is a widget that displays a list of items with a fixed extent inside a `CustomScrollView`. By default, it comes with its own scroll physics, which control the behavior of scrolling. However, there might be cases where you want to apply custom scroll physics to achieve a specific scrolling effect.

Here is an example of how to apply custom scroll physics to a `SliverFixedExtentList` in Flutter:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/physics.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom Scroll Physics',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  final ScrollController _scrollController = ScrollController(
    initialScrollOffset: 0,
    keepScrollOffset: true,
  );

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Scroll Physics'),
      ),
      body: CustomScrollView(
        slivers: [
          SliverFixedExtentList(
            itemExtent: 100.0,
            delegate: SliverChildBuilderDelegate(
              (BuildContext context, int index) {
                return ListTile(
                  title: Text('Item $index'),
                );
              },
              childCount: 10,
            ),
            physics: CustomScrollPhysics(),
            controller: _scrollController,
          ),
        ],
      ),
    );
  }
}

class CustomScrollPhysics extends ScrollPhysics {
  @override
  CustomScrollPhysics({ScrollPhysics? parent}) : super(parent: parent);

  @override
  CustomScrollPhysics applyTo(ScrollPhysics? ancestor) {
    return CustomScrollPhysics(parent: buildParent(ancestor!));
  }

  @override
  Simulation createBallisticSimulation(
    ScrollMetrics position,
    double velocity,
  ) {
    return BouncingScrollSimulation(
      spring: 1000.0,
      position: position.pixels,
      velocity: velocity,
    );
  }
}
```

In the above code, we create a `HomePage` widget which contains a `CustomScrollView`. Inside the `CustomScrollView`, we have a single `SliverFixedExtentList` that displays a list of `ListTile` widgets. We apply custom scroll physics to the `SliverFixedExtentList` in the `physics` property.

The `CustomScrollPhysics` class extends `ScrollPhysics` and overrides the `createBallisticSimulation` method, which determines the behavior of scrolling when the user releases their finger. In this example, we use the `BouncingScrollSimulation` to create a bouncing effect when scrolling. You can customize the scroll physics according to your requirements.

Remember to add any necessary packages to your `pubspec.yaml` file and import them in your code.

With this custom scroll physics, you can achieve different scrolling effects, such as bouncing or overscrolling, for your `SliverFixedExtentList` in Flutter.

#flutter #scrollphysics
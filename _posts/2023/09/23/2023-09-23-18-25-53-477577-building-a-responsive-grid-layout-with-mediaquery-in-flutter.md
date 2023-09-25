---
layout: post
title: "Building a responsive grid layout with `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [responsivelayout]
comments: true
share: true
---

In today's blog post, we will explore how to create a responsive grid layout using the `MediaQuery` class in Flutter. Building responsive layouts is crucial in modern app development, as it allows our app to adapt to various screen sizes and orientations seamlessly. Flutter provides powerful tools to achieve this, and one such tool is the `MediaQuery` class.

## What is `MediaQuery`?

The `MediaQuery` class in Flutter gives us access to the current media information, such as screen size, orientation, and pixel density. It allows us to make design decisions based on the device's characteristics, providing a responsive user interface.

## Setting up the Grid Layout

First, let's create a new Flutter project and set up the necessary files. Open your favorite code editor and create a new Flutter project.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive Grid Layout'),
        ),
        body: GridWidget(), // Create a new widget for the grid layout
      ),
    );
  }
}
```

## Implementing the Responsive Grid Layout

Now, let's create a new widget called `GridWidget` that will display our responsive grid layout. Inside the `GridWidget` class, we will create a function called `_buildGridTile` that will take a `String` as an argument and return a `GridTile` widget.

```dart
class GridWidget extends StatelessWidget {
  // Create a list of items for the grid
  final List<String> items = ['Item 1', 'Item 2', 'Item 3', 'Item 4', 'Item 5'];

  // Function to build the grid tiles
  Widget _buildGridTile(String item) {
    return GridTile(
      child: Container(
        color: Colors.blue,
        child: Center(
          child: Text(
            item,
            style: const TextStyle(color: Colors.white, fontSize: 20),
          ),
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    // Get the current screenSize from the MediaQuery
    final screenSize = MediaQuery.of(context).size;

    // Calculate the number of columns based on the screen width
    final columns = (screenSize.width / 200).floor();

    return GridView.count(
      crossAxisCount: columns,
      children: items.map((item) => _buildGridTile(item)).toList(),
    );
  }
}
```

In the above code, we have created a list of items for the grid. We then create the `_buildGridTile` function that takes an item and returns a styled `GridTile` widget. In the `build` method, we retrieve the `screenSize` using `MediaQuery.of(context).size` and calculate the number of columns based on the width of the screen.

Finally, we use `GridView.count` widget to create a responsive grid layout. It takes the number of columns and a list of grid tiles as children.

## Testing the Responsive Grid Layout

Save the changes and run the Flutter app on your device or simulator. You will see a responsive grid layout with the number of columns adjusting based on the screen width.

By utilizing the `MediaQuery` class and `GridView` widget, we have successfully built a responsive grid layout in Flutter. This technique allows our app to adapt to various screen sizes and provides optimal user experience.

Give it a try in your next Flutter project and start creating beautiful and responsive UIs effortlessly!

#flutter #responsivelayout
---
layout: post
title: "How to use the Opacity widget to create a transparent background for a widget"
description: " "
date: 2023-09-25
tags: [Flutter, Opacity]
comments: true
share: true
---

In this tutorial, we will explore how to use the `Opacity` widget in a Flutter application to create a transparent background for a widget. The `Opacity` widget allows us to adjust the transparency level of its child widget, making it easy to create visually appealing UIs with varying degrees of transparency.

## Step 1: Create a Flutter Project

To get started, let's create a new Flutter project. Open your terminal or command prompt and run the following command:

```
flutter create transparent_background_widget
```

This will initialize a new Flutter project with the name `transparent_background_widget`.

## Step 2: Modify the MaterialApp Widget

Open the `lib/main.dart` file in your project and modify the `build()` method of the `MyApp` class as follows:

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
          title: Text('Transparent Background'),
        ),
        body: Center(
          child: Opacity(
            opacity: 0.5,
            child: Container(
              width: 200,
              height: 200,
              color: Colors.blue,
            ),
          ),
        ),
      ),
    );
  }
}
```

In the code above, we've used the `Opacity` widget to create a transparent background for a `Container` widget. The `opacity` property is set to `0.5`, which indicates that the child widget (the blue `Container`) should be 50% transparent.

## Step 3: Run the Application

Save the `main.dart` file and run the application using the following command:

```
flutter run
```

You should now see a blue square with a transparent background in the center of the screen. The transparency level can be adjusted by changing the `opacity` value in the `Opacity` widget.

## Conclusion

In this tutorial, we learned how to use the `Opacity` widget in Flutter to create a transparent background for a widget. You can now experiment with different transparency levels and create visually appealing UIs with varying degrees of transparency.

#Flutter #UI #Opacity
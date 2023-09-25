---
layout: post
title: "Building a responsive bottom sheet with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [responsivebottomsheet]
comments: true
share: true
---

In this blog post, we will learn how to build a responsive bottom sheet using the `MediaQuery` widget in Flutter. A bottom sheet is a common user interface pattern used to display extra information or quick actions at the bottom of the screen.

## Prerequisites

To follow along with this tutorial, make sure you have Flutter installed on your machine. You can find the installation instructions on the [Flutter website](https://flutter.dev).

## Getting Started

Let's start by creating a new Flutter project. Open your terminal and run the following command:

```bash
flutter create responsive_bottom_sheet
```

This will create a new Flutter project in a directory named `responsive_bottom_sheet`. Navigate to the project directory using the `cd` command:

```bash
cd responsive_bottom_sheet
```

Now, open the `lib/main.dart` file in a text editor and delete the default code. We're going to start from scratch.

## Implementing the Bottom Sheet

First, let's define a simple `HomePage` widget as the entry point of our application. We will wrap it with a `Scaffold` widget to provide the basic layout structure.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Bottom Sheet'),
      ),
      body: Center(
        child: Text('Hello, world!'),
      ),
    );
  }
}
```

Now, let's add a button at the bottom of the screen to show the bottom sheet when pressed. We will use a `FloatingActionButton` for this purpose.

```dart
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Bottom Sheet'),
      ),
      body: Center(
        child: Text('Hello, world!'),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          showModalBottomSheet(
            context: context,
            builder: (BuildContext context) {
              return Container(
                height: 200,
                child: Center(
                  child: Text('This is a bottom sheet'),
                ),
              );
            },
          );
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

In the `onPressed` callback of the `FloatingActionButton`, we call the `showModalBottomSheet` function to display the bottom sheet. The `builder` parameter is used to build the content of the bottom sheet, which is a simple `Container` in this case.

## Making the Bottom Sheet Responsive

Now, let's make the bottom sheet responsive using the `MediaQuery` widget. We can use `MediaQuery.of(context).size.height` to get the height of the screen and adjust the height of the bottom sheet accordingly.

Replace the `Container` widget in the `builder` method with the following code:

~~~dart
Container(
  height: MediaQuery.of(context).size.height * 0.5,
  child: Center(
    child: Text('This is a responsive bottom sheet'),
  ),
),
~~~

Here, we set the height of the `Container` to half the height of the screen using `MediaQuery.of(context).size.height * 0.5`. This ensures that the bottom sheet will take up only half of the screen regardless of the device size.

That's it! You have successfully built a responsive bottom sheet using the `MediaQuery` widget in Flutter.

## Conclusion

In this tutorial, we learned how to create a responsive bottom sheet in Flutter using the `MediaQuery` widget. We started by setting up a basic Flutter project, implemented a simple bottom sheet with a show button, and made the bottom sheet responsive by using `MediaQuery` to adjust its height based on the device screen size.

Remember to always make your user interfaces responsive to provide a consistent user experience across different devices.

Happy coding!

#flutter #responsivebottomsheet
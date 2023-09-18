---
layout: post
title: "Building a horizontal carousel using ListView in Flutter."
description: " "
date: 2023-09-15
tags: [carousel]
comments: true
share: true
---

In this tutorial, we will learn how to create a horizontal carousel using the `ListView` widget in Flutter. A carousel is a popular UI element that allows users to scroll through a set of items horizontally. By building a carousel, you can showcase multiple items in a compact and visually appealing way.

## Prerequisites
To follow along with this tutorial, you should have a basic understanding of Flutter and have Flutter installed on your system. If you haven't installed Flutter yet, you can refer to the official documentation for instructions.

## Getting Started
1. Create a new Flutter project using the Flutter command-line interface (CLI) or your preferred IDE.
2. Open the project in your preferred code editor.

## Building the Carousel
1. Open the `lib/main.dart` file and remove the default code from the `main()` function.
2. Define a list of items that you want to display in the carousel. For simplicity, we will use a list of strings.

```dart
List<String> items = [
  "Item 1",
  "Item 2",
  "Item 3",
  "Item 4",
  "Item 5",
];
```

## Using ListView.Builder
Flutter provides the `ListView.builder` widget, which is ideal for building dynamic lists efficiently. Let's use this widget to build our carousel.

3. Replace the `build()` method of the `MyApp` class with the following code:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Carousel',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Horizontal Carousel'),
        ),
        body: ListView.builder(
          scrollDirection: Axis.horizontal,
          itemCount: items.length,
          itemBuilder: (context, index) {
            return Container(
              width: 200,
              margin: EdgeInsets.all(8),
              color: Colors.blue,
              child: Center(
                child: Text(
                  items[index],
                  style: TextStyle(
                    color: Colors.white,
                    fontSize: 24,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
            );
          },
        ),
      ),
    );
  }
}
```

In the `ListView.builder`, we set the `scrollDirection` property to `Axis.horizontal` to enable horizontal scrolling. We also specify the `itemCount` as the length of the items list and define the `itemBuilder` function to return a container with the appropriate content for each item.

4. Save the file and run the app using `flutter run` in the terminal or your IDE's run command. You will see the horizontal carousel with the items displayed.

## Customizing the Carousel
Now that you have the basic version of the carousel in place, you can customize it according to your needs. Here are a few suggestions:

- Adjust the width and height of the container to fit your items.
- Customize the styling of the text inside the container.
- Add images or icons instead of text.
- Add interactivity by wrapping each item in a GestureDetector widget and handling gestures.

By following this tutorial, you have learned how to build a horizontal carousel using the `ListView` widget in Flutter. You can now enhance and customize the carousel according to your app's requirements. Happy coding!

#flutter #carousel
---
layout: post
title: "Implementing responsive swipeable cards using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: []
comments: true
share: true
---

In this tutorial, we will learn how to implement responsive swipeable cards using `MediaQuery` in Flutter. Swipeable cards are a common UI feature that allows users to swipe left or right to interact with content. We will create a card stack that adapts its layout based on the device screen size.

![Swipeable Cards](https://example.com/swipeable-cards.png)

## Prerequisites

To follow along with this tutorial, you should have a basic understanding of Flutter and how to set up a Flutter project. If you're new to Flutter, please refer to the official Flutter documentation for installation and setup instructions.

## Getting Started

Let's start by creating a new Flutter project. Open your terminal and execute the following command:

```dart
flutter create swipeable_cards
```

Change your directory to the newly created project:

```dart
cd swipeable_cards
```

Now, we can open the project in your preferred code editor and start building our swipeable cards.

## Building the Card Stack

First, we need to import the necessary packages for our project. Open `pubspec.yaml` and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_swiper: ^1.1.6
```

Save the file and run the following command to install the packages:

```dart
flutter pub get
```

Next, open `lib/main.dart` and replace the default code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_swiper/flutter_swiper.dart';

void main() {
  runApp(SwipeableCardsApp());
}

class SwipeableCardsApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Swipeable Cards',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: SwipeableCardsScreen(),
    );
  }
}

class SwipeableCardsScreen extends StatefulWidget {
  @override
  _SwipeableCardsScreenState createState() => _SwipeableCardsScreenState();
}

class _SwipeableCardsScreenState extends State<SwipeableCardsScreen> {
  final List<String> cards = [
    'Card 1',
    'Card 2',
    'Card 3',
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Swipeable Cards'),
      ),
      body: Swiper(
        itemBuilder: (BuildContext context, int index) {
          return Card(
            child: Center(
              child: Text(
                cards[index],
                style: TextStyle(
                  fontSize: 24.0,
                ),
              ),
            ),
          );
        },
        itemCount: cards.length,
        pagination: SwiperPagination(),
        control: SwiperControl(),
      ),
    );
  }
}
```

In the above code, we've defined the `SwipeableCardsApp` and `SwipeableCardsScreen` classes. We are using the `flutter_swiper` package to implement the swipeable cards. The `cards` list stores the content for each card.

Inside the `build` method of `SwipeableCardsScreen`, we have wrapped the `Swiper` widget with a `Scaffold` widget. The `Swiper` widget is responsible for building the swipeable card stack. We have also added a basic `AppBar` for the screen title.

Save the file, and you can now run the app using the following command:

```dart
flutter run
```

You should see a screen with the swipeable card stack. You can swipe left or right to navigate through the cards.

## Making the Cards Responsive

Now we will make the swipeable cards responsive by adapting the layout based on the device screen size. We will use the `MediaQuery` class to get the screen dimensions and adjust the card size accordingly.

First, import the `MediaQuery` class at the top of the `main.dart` file:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_swiper/flutter_swiper.dart';
```

Then, modify the `build` method of the `_SwipeableCardsScreenState` class as follows:

```dart
@override
Widget build(BuildContext context) {
  final screenWidth = MediaQuery.of(context).size.width;
  final screenHeight = MediaQuery.of(context).size.height;

  return Scaffold(
    appBar: AppBar(
      title: Text('Swipeable Cards'),
    ),
    body: Swiper(
      itemBuilder: (BuildContext context, int index) {
        final cardWidth = screenWidth * 0.8;
        final cardHeight = screenHeight * 0.5;

        return Card(
          child: Container(
            width: cardWidth,
            height: cardHeight,
            child: Center(
              child: Text(
                cards[index],
                style: TextStyle(
                  fontSize: 24.0,
                ),
              ),
            ),
          ),
        );
      },
      itemCount: cards.length,
      pagination: SwiperPagination(),
      control: SwiperControl(),
    ),
  );
}
```

In the above code, we calculate the `screenWidth` and `screenHeight` using the `MediaQuery` class. Then, we define `cardWidth` and `cardHeight` based on these dimensions.

We set the width and height of the card container using these calculated values.

Save the file and run the app using `flutter run`. You will now see that the card stack adapts its size based on the device screen size.

## Conclusion

In this tutorial, we have learned how to implement responsive swipeable cards using `MediaQuery` in Flutter. We built a card stack that adapts its layout based on the device screen size, allowing users to swipe left or right to interact with the content.

Feel free to experiment with different card designs and further customize the swipeable cards to suit your app's needs.
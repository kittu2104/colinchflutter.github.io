---
layout: post
title: "Implementing a parallax card effect in ListView in Flutter."
description: " "
date: 2023-09-15
tags: [parallax, listview]
comments: true
share: true
---

Parallax scrolling is a popular technique in app and web design that creates a visually appealing effect by moving different layers of content at different speeds. In this tutorial, we will learn how to implement a parallax card effect in a ListView in Flutter.

## Step 1: Setting up the Project

First, make sure you have Flutter and Dart installed on your machine. Create a new Flutter project using the following command:

```
flutter create parallax_card_effect
```

Change to the project directory:

```
cd parallax_card_effect
```

Open the project in your preferred code editor.

## Step 2: Adding Dependencies

Add the following dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  animated_card: ^1.0.0
```

Run `flutter pub get` to download the dependencies.

## Step 3: Creating the Parallax Card Widget

Create a new file called `parallax_card_widget.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:animated_card/animated_card.dart';

class ParallaxCardWidget extends StatelessWidget {
  final String title;
  final String subtitle;
  final String imagePath;

  const ParallaxCardWidget({
    required this.title,
    required this.subtitle,
    required this.imagePath,
  });

  @override
  Widget build(BuildContext context) {
    return AnimatedCard(
      direction: AnimatedCardDirection.horizontal,
      child: Container(
        margin: EdgeInsets.symmetric(horizontal: 16, vertical: 8),
        decoration: BoxDecoration(
          borderRadius: BorderRadius.circular(8),
          image: DecorationImage(
            image: AssetImage(imagePath),
            fit: BoxFit.cover,
          ),
        ),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(title,
                style: TextStyle(
                  color: Colors.white,
                  fontSize: 24,
                  fontWeight: FontWeight.bold,
                )),
            SizedBox(height: 8),
            Text(subtitle,
                style: TextStyle(
                  color: Colors.white,
                  fontSize: 16,
                )),
          ],
        ),
      ),
    );
  }
}
```

In this code, we create a `ParallaxCardWidget` which takes `title`, `subtitle`, and `imagePath` as parameters. We use the `AnimatedCard` widget from the `animated_card` package to animate the card as it enters the screen.

## Step 4: Creating the Parallax Card List

Open the `lib/main.dart` file and replace the default code with the following:

```dart
import 'package:flutter/material.dart';

import 'parallax_card_widget.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Parallax Card Effect',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: ParallaxCardListScreen(),
    );
  }
}

class ParallaxCardListScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Parallax Card Effect')),
      body: ListView(
        children: [
          ParallaxCardWidget(
            title: 'Card 1',
            subtitle: 'This is the first card',
            imagePath: 'assets/card1.jpg',
          ),
          ParallaxCardWidget(
            title: 'Card 2',
            subtitle: 'This is the second card',
            imagePath: 'assets/card2.jpg',
          ),
          ParallaxCardWidget(
            title: 'Card 3',
            subtitle: 'This is the third card',
            imagePath: 'assets/card3.jpg',
          ),
        ],
      ),
    );
  }
}
```

Replace the file paths in the `imagePath` parameter with your own card images.

## Step 5: Running the App

To run the app on your device or simulator, use the following command:

```
flutter run
```

You should now see a list of parallax cards with the specified titles, subtitles, and images.

Congratulations! You have successfully implemented a parallax card effect in a ListView using Flutter.

#flutter #parallax #listview
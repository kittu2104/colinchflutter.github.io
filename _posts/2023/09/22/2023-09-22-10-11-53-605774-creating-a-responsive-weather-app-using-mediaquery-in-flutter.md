---
layout: post
title: "Creating a responsive weather app using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [responsiveapp]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive weather app using `MediaQuery` in Flutter. With `MediaQuery`, we can build apps that adapt to different screen sizes. 

## Prerequisites
Before getting started, make sure you have Flutter SDK installed on your machine and a basic understanding of Flutter development.

## Setting Up the Project
1. Create a new Flutter project by running the following command in your terminal:
```bash
flutter create weather_app
```
2. Open the project in your preferred code editor.

## Building the Weather App
1. Open the `lib/main.dart` file.
2. Remove the default code and replace it with the code below:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(WeatherApp());
}

class WeatherApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Weather App',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: WeatherScreen(),
    );
  }
}

class WeatherScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Weather'),
      ),
      body: Center(
        child: Text(
          'Weather information will be displayed here.',
        ),
      ),
    );
  }
}
```

3. Save the file and run the app using the command:
```bash
flutter run
```

## Creating a Responsive Layout
1. Wrap the `Scaffold` widget in `LayoutBuilder` widget to access the parent widget's constraints:
```dart
class WeatherScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return LayoutBuilder(builder: (context, constraints) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Weather'),
        ),
        body: Center(
          child: Text(
            'Weather information will be displayed here.',
          ),
        ),
      );
    });
  }
}
```

2. Use `MediaQuery.of()` method to access the screen size and apply responsive changes:
```dart
class WeatherScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return LayoutBuilder(builder: (context, constraints) {
      final double screenWidth = MediaQuery.of(context).size.width;

      return Scaffold(
        appBar: AppBar(
          title: Text('Weather'),
        ),
        body: Center(
          child: Text(
            'Screen Width: $screenWidth',
          ),
        ),
      );
    });
  }
}
```

3. Save the file and run the app again. You will now see the screen width being displayed in the center of the screen.

## Conclusion
In this tutorial, we learned how to create a responsive weather app using `MediaQuery` in Flutter. With `MediaQuery`, we were able to access the screen size and apply responsive changes to our app's layout. Feel free to enhance the app by fetching real-time weather data and customizing the UI.

#flutter #responsiveapp